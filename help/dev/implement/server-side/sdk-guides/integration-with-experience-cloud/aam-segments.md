---
title: Integratie met Experience Cloud AAM
description: Integratie met Experience Cloud, integratie met Audience Manager
keywords: levering api, server-kant, serverkant, integratie, publieksmanager, am
exl-id: c21e0200-23ba-4a0b-adf4-38e03c087f00
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# AAM

[!DNL Adobe Audience Manager] segmenten kunnen worden benut via [!DNL Adobe Target] SDK&#39;s. Om AAM segmenten te benutten, moeten de volgende velden worden ingevuld:

>[!NOTE]
>
>AAM segmenten worden niet ondersteund voor beslissingsactiviteiten op het apparaat.

| Veldnaam | Vereist | Beschrijving |
| --- | --- | --- |
| `locationHint` | Ja | De Hint van de Plaats DCS wordt gebruikt om te bepalen welke AAM DCS Eindpunt om te slaan om het profiel terug te winnen. Moet >= 1 zijn. |
| `marketingCloudVisitorId` | Ja | Bezoeker-id Marketing Cloud |
| `blob` | Ja | AAM Blob wordt gebruikt om aanvullende gegevens naar AAM te verzenden. Mag niet leeg zijn en de grootte &lt;= 1024. |

De SDK vult deze velden automatisch voor u in wanneer u een `getOffers` methodevraag, maar u zult een geldig bezoekerskoekje moeten verzekeren wordt verstrekt. Voor dit cookie moet u VisitorAPI.js implementeren in de browser.

## Handleiding implementatie

### Gebruik van cookies

Cookies worden gebruikt voor correlaties [!DNL Adobe Audience Manager] verzoeken met [!DNL Adobe Target] verzoeken. Dit zijn de cookies die in deze implementatie worden gebruikt.

| Cookie | Naam | Beschrijving |
| --- | --- | --- |
| bezoekerscookie | `AMCVS_XXXXXXXXXXXXXXXXXXXXXXXX%40AdobeOrg` | Deze cookie wordt ingesteld door `VisitorAPI.js` wanneer deze wordt geïnitialiseerd met `visitorState` van het doel `getOffers` reactie. |
| doelcookie | `mbox` | Uw webserver moet dit cookie instellen met de naam en waarde van `targetCookie` van het doel `getOffers` reactie. |

### Overzicht van stappen

Stel dat een gebruiker een URL invoert in een browser die een aanvraag naar uw webserver verzendt. Bij het voldoen aan dat verzoek:

1. De server leest de bezoeker en doelcookies uit de aanvraag.
1. De server roept de `getOffers` van de [!DNL Target] SDK, met vermelding van de bezoeker en doelcookies, indien beschikbaar.
1. Wanneer de `getOffers` aanroep is uitgevoerd, waarden voor `targetCookie` en `visitorState` worden gebruikt.
   1. Een cookie wordt ingesteld op de reactie met waarden die zijn genomen van `targetCookie`. Dit doet u met de opdracht `Set-Cookie` responsheader, die de browser opgeeft het doelcookie te blijven gebruiken.
   1. Er wordt een HTML-reactie voorbereid die wordt geïnitialiseerd `VisitorAPI.js` en passeert `visitorState` van de doelrespons.
1. De HTML-reactie wordt in de browser geladen..
   1. `VisitorAPI.js` is opgenomen in de koptekst van het document.
   1. Bezoeker-API is geïnitialiseerd met `visitorState` van de `getOffers` SDK-reactie. Hierdoor wordt het bezoekerscookie ingesteld in de browser, zodat deze op volgende aanvragen naar de server wordt verzonden.

### Voorbeeldcode

Het volgende codevoorbeeld voert elk van de hierboven geschetste stappen uit. Elke stap wordt in de code weergegeven als een inlineopmerking naast de implementatie.

#### Node.js

Dit voorbeeld is afhankelijk van [express, een Node.js-webframework](https://expressjs.com/).

>[!BEGINTABS]

>[!TAB server.js]

```js {line-numbers="true"}
const fs = require("fs");
const express = require("express");
const cookieParser = require("cookie-parser");
const Handlebars = require("handlebars");
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  timeout: 10000,
  logger: console,
};
const targetClient = TargetClient.create(CONFIG);
const TEMPLATE = fs.readFileSync(`${__dirname}/index.handlebars`).toString();
const handlebarsTemplate = Handlebars.compile(TEMPLATE);

Handlebars.registerHelper("toJSON", function (object) {
  return new Handlebars.SafeString(JSON.stringify(object, null, 4));
});

const app = express();
app.use(cookieParser());
app.use(express.static(__dirname + "/public"));

app.get("/", async (req, res) => {
  // The server reads the visitor and target cookies from the request.
  const visitorCookie =
    req.cookies[
      encodeURIComponent(
        TargetClient.getVisitorCookieName(CONFIG.organizationId)
      )
    ];
  const targetCookie = req.cookies[TargetClient.TargetCookieName];
  const address = { url: req.headers.host + req.originalUrl };

  const targetRequest = {
    execute: {
      mboxes: [
        { name: "homepage", index: 1, address },
        { name: "SummerShoesOffer", index: 2, address },
        { name: "SummerDressOffer", index: 3, address }
      ],
    },
  };

  res.set({
    "Content-Type": "text/html",
    Expires: new Date().toUTCString(),
  });

  try {
    // The server makes a call to the `getOffers` method of the Target SDK specifying the visitor and target cookies if available.
    const targetResponse = await targetClient.getOffers({
      request: targetRequest,
      visitorCookie,
      targetCookie,
    });

    // When the `getOffers` call is fulfilled, values for `targetCookie` and `visitorState` from the response are used.
    // A cookie is set on the response with values taken from `targetCookie`.  This is done using the `Set-Cookie` response header which tells the browser to persist the target cookie.
    res.cookie(
      targetResponse.targetCookie.name,
      targetResponse.targetCookie.value,
      { maxAge: targetResponse.targetCookie.maxAge * 1000 }
    );

    // An HTML response is prepared that initializes VisitorAPI.js and passes in `visitorState` from the target response.
    const html = handlebarsTemplate({
      organizationId: CONFIG.organizationId,
      targetResponse,
    });

    res.status(200).send(html);
  } catch (error) {
    console.error("Target:", error);
    res.status(500).send(error);
  }
});

app.listen(3000, function () {
  console.log("Listening on port 3000 and watching!");
});
```

>[!TAB index.handlebars]

```html {line-numbers="true"}
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) Integration Sample</title>

  <!-- VisitorAPI.js is included in the document header. -->
  <script src="VisitorAPI.js"></script>
  <script>
    // VisitorAPI is initialized with visitorState from the `getOffers` SDK response. This will cause the visitor cookie to be set in the browser so it will be sent to the server on subsequent requests.
    Visitor.getInstance("{{organizationId}}", {serverState: {{toJSON targetResponse.visitorState}} });
  </script>
</head>
<body>
  <h1>response</h1>
  <pre>{{toJSON targetResponse}}</pre>
</body>
</html>
```

>[!ENDTABS]

#### Java

Dit voorbeeld gebruikt [lente, een Java-webframework](https://spring.io/).

>[!BEGINTABS]

>[!TAB ClientSampleApplication.java]

```java {line-numbers="true"}
@SpringBootApplication
public class ClientSampleApplication {

    public static void main(String[] args) {
        System.setProperty(SimpleLogger.DEFAULT_LOG_LEVEL_KEY, "DEBUG");
        SpringApplication.run(ClientSampleApplication.class, args);
    }

    @Bean
    TargetClient marketingCloudClient() {
        ClientConfig clientConfig = ClientConfig.builder()
                .client("acmeclient")
                .organizationId("1234567890@AdobeOrg")
                .defaultDecisioningMethod(DecisioningMethod.SERVER_SIDE)
                .build();

        return TargetClient.create(clientConfig);
    }
}
```

>[!TAB TargetController.java]

```java {line-numbers="true"}
@Controller
@RequestMapping("/")
public class TargetController {

    @Autowired
    private TargetClientService targetClientService;

    @GetMapping
    public String index(Model model, HttpServletRequest request, HttpServletResponse response) {
        // The server reads the visitor and target cookies from the request.
        List<TargetCookie> targetCookies = getTargetCookies(request.getCookies());

        Address address = getAddress(request);

        List<MboxRequest> mboxRequests = new ArrayList<>();
        mboxRequests.add((MboxRequest) new MboxRequest().name("homepage").index(1).address(address));
        mboxRequests.add((MboxRequest) new MboxRequest().name("SummerShoesOffer").index(2).address(address));
        mboxRequests.add((MboxRequest) new MboxRequest().name("SummerDressOffer").index(3).address(address));

        TargetDeliveryResponse targetDeliveryResponse = targetClientService.getOffers(mboxRequests, targetCookies, request,
                response);

        // An HTML response is prepared that initializes VisitorAPI.js and passes in `visitorState` from the target response.
        model.addAttribute("visitorState", targetDeliveryResponse.getVisitorState());
        model.addAttribute("targetResponse", targetDeliveryResponse);
        model.addAttribute("organizationId", "1234567890@AdobeOrg");

        return "index";
    }
}
```

>[!TAB TargetClientService.java]

```java {line-numbers="true"}
@Service
public class TargetClientService {

    private final TargetClient targetJavaClient;

    public TargetClientService(TargetClient targetJavaClient) {
        this.targetJavaClient = targetJavaClient;
    }

    public TargetDeliveryResponse getOffers(List<MboxRequest> executeMboxes, List<TargetCookie> cookies, HttpServletRequest request, HttpServletResponse response) {

        Context context = getContext(request);
        ExecuteRequest executeRequest = new ExecuteRequest();
        executeRequest.setMboxes(executeMboxes);

        TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
                .context(context)
                .execute(executeRequest)
                .cookies(cookies)
                .build();

        // The server makes a call to the `getOffers` method of the Target SDK specifying the visitor and target cookies if available.
        TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);

        // When the `getOffers` call is fulfilled, values for `targetCookie` and `visitorState` from the response are used.
        // A cookie is set on the response with values taken from `targetCookie`.  This is done using the `Set-Cookie` response header which tells the browser to persist the target cookie.
        setCookies(targetResponse.getCookies(), response);
        return targetResponse;
    }
}
```

>[!TAB TargetRequestUtils.java]

```java {line-numbers="true"}
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Target Only : GetOffer</title>

    <!-- VisitorAPI.js is included in the document header. -->
    <script src="../../js/VisitorAPI.js"></script>
    <script th:inline="javascript">
        // VisitorAPI is initialized with visitorState from the `getOffers` SDK response. This will cause the visitor cookie to be set in the browser so it will be sent to the server on subsequent requests.
        Visitor.getInstance(/*[[${organizationId}]]*/ "", {serverState: /*[[${visitorState}]]*/ {}});
    </script>
</head>
<body>
    <h1>response</h1>
    <pre>[[${targetResponse}]]</pre>
</body>
</html>
```

>[!ENDTABS]

Voor meer informatie over TargetRequestUtils.java, zie [Hulpprogrammamethoden (Java)](https://experienceleague.corp.adobe.com/docs/target-dev/developer/server-side/java/utility-methods.html){target=_blank}
