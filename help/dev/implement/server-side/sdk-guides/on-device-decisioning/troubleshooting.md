---
title: Beslissing op apparaat oplossen
description: Leer hoe u problemen kunt oplossen [!UICONTROL on-device decisioning]
exl-id: e76f95ce-afae-48e0-9dbb-2097133574dc
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 0%

---

# Problemen oplossen [!UICONTROL on-device decisioning]

## Configuratie valideren

### Overzicht van stappen

1. Zorg ervoor dat `logger` is geconfigureerd
1. Zorgen [!DNL Target] traces is ingeschakeld
1. Controleer de [!UICONTROL on-device decisioning] *regelartefact* is opgehaald en in cache geplaatst volgens het gedefinieerde pollinginterval.
1. Valideer de levering van inhoud via het in de cache geplaatste regelartefact door een test te creëren [!UICONTROL on-device decisioning] activiteit via de op formulier gebaseerde ervaringscomposer.
1. Inspect verzendt meldingsfouten

## 1. Zorg ervoor dat het logger is geconfigureerd

Zorg er bij het initialiseren van de SDK voor dat u logboekregistratie inschakelt.

**Node.js**

Voor Node.js SDK a `logger` -object moet worden opgegeven.

```js {line-numbers="true"}
const CONFIG = {
  client: "<your client code>",
  organizationId: "<your organization ID>",
  logger: console
};
```

**Java SDK**

Voor Java SDK `logRequests` op de `ClientConfig` moet zijn ingeschakeld.

```js {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("<your client code>")
  .organizationId("<your organization ID>")
  .logRequests(true)
  .build();
```

De JVM moet ook worden gestart met de volgende opdrachtregelparameter:

```bash {line-numbers="true"}
java -Dorg.slf4j.simpleLogger.defaultLogLevel=DEBUG ...
```

## 2. Zorgen[!DNL Target]Traces is ingeschakeld

Als u sporen inschakelt, wordt aanvullende informatie van [!DNL Adobe Target] wat betreft de artefact.

1. Ga naar de[!DNL Target]UI in [!DNL Experience Cloud].

   ![alternatieve afbeelding](assets/asset-target-ui-1.png)

1. Navigeren naar **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** en klik op **[!UICONTROL Generate New Authorization Token]**.

   ![alternatieve afbeelding](assets/asset-target-ui-2.png)

1. Kopieer het nieuwe machtigingstoken naar het klembord en voeg het toe aan uw[!DNL Target]verzoek:

   **Node.js**

   ```js {line-numbers="true"}
   const request = {
     trace: {
       authorizationToken: "88f1a924-6bc5-4836-8560-2f9c86aeb36b"
     },
     execute: {
       mboxes: [{
         name: "sdk-mbox"
       }]
   }};
   ```

   **Java**

   ```js {line-numbers="true"}
   Trace trace = new Trace()
     .authorizationToken("88f1a924-6bc5-4836-8560-2f9c86aeb36b");
   Context context = new Context()
     .channel(ChannelType.WEB);
   MboxRequest mbox = new MboxRequest()
     .name("sdk-mbox")
     .index(0);
   ExecuteRequest executeRequest = new ExecuteRequest()
     .mboxes(Arrays.asList(mbox));
   
   TargetDeliveryRequest request = TargetDeliveryRequest.builder()
     .trace(trace)
     .context(context)
     .execute(executeRequest)
     .build();
   ```

1. Start uw app en controleer de serverterminal terwijl de registreerfunctie en tracering zijn ingeschakeld. De volgende output van registreerder bevestigt dat het regelartefact is teruggewonnen:

   **Node.js SDK**

   ```text {line-numbers="true"}
     AT: LD.ArtifactProvider fetching artifact - https://assets.adobetarget.com/your-client-code/production/v1/rules.json
     AT: LD.ArtifactProvider artifact received - status=200
   ```

## 3. Controleer de [!UICONTROL on-device decisioning] *regelartefact* is opgehaald en in cache geplaatst volgens het gedefinieerde pollinginterval.

1. Wacht de duur van het opiniepeilingsinterval (gebrek is 5 minuten) en zorg ervoor dat het artefact door SDK wordt gehaald. De zelfde eindlogboeken zullen output zijn.

   Daarnaast wordt informatie van de[!DNL Target]Het spoor zou aan de terminal met details over het regelartefact moeten worden uitgevoerd.

   ```text {line-numbers="true"}
   "trace": {
     "clientCode": "your-client-code",
     "artifact": {
       "artifactLocation": "https://assets.adobetarget.com/your-client-code/production/v1/rules.json",
       "pollingInterval": 300000,
       "pollingHalted": false,
       "artifactVersion": "1.0.0",
       "artifactRetrievalCount": 10,
       "artifactLastRetrieved": "2020-09-20T00:09:42.707Z",
       "clientCode": "your-client-code",
       "environment": "production",
       "generatedAt": "2020-09-22T17:17:59.783Z"
     },
   ```

## 4. Valideer de levering van inhoud via het caching regelartefact door een test te creëren [!UICONTROL on-device decisioning] activiteit via de op formulier gebaseerde ervaringscomposer

1. Ga naar de[!DNL Target]UI in Experience Cloud

   ![alternatieve afbeelding](assets/asset-target-ui-1.png)

1. Maak een nieuwe XT-activiteit met behulp van de Form-based Experience Composer.

   ![alternatieve afbeelding](assets/asset-form-base-composer-ui.png)

1. Voer de naam van het selectievakje in die in de[!DNL Target]aanvraag als de locatie voor de XT-activiteit (let op: dit moet een unieke naam van een box zijn, specifiek voor ontwikkelingsdoeleinden).

   ![alternatieve afbeelding](assets/asset-mbox-location-ui.png)

1. Wijzig de inhoud in een HTML-voorstel of een JSON-voorstel. Dit wordt geretourneerd in het dialoogvenster[!DNL Target]verzoek aan uw toepassing. Geef voor de activiteit de focus op als Alle bezoekers en selecteer de gewenste metrische waarde. Geef een naam op voor de activiteit, sla deze op en activeer deze vervolgens om ervoor te zorgen dat de box/locatie in gebruik alleen voor ontwikkeling is.

   ![alternatieve afbeelding](assets/asset-target-content-ui.png)

1. Voeg in uw toepassing een logboekinstructies toe voor de inhoud die wordt ontvangen in het antwoord van uw[!DNL Target]verzoek

   **Node.js SDK**

   ```js {line-numbers="true"}
   try {
     const response = await targetClient.getOffers({ request });
     console.log('Response: ', response.response.execute.mboxes[0].options[0].content);
   } catch (error) {
     console.error('Something went wrong', error);
   }
   ```

   **Java SDK**

   ```js {line-numbers="true"}
   try {
     Context context = new Context()
       .channel(ChannelType.WEB);
     MboxRequest mbox = new MboxRequest()
       .name("sdk-mbox")
       .index(0);
     ExecuteRequest executeRequest = new ExecuteRequest()
       .mboxes(Arrays.asList(mbox));
   
     TargetDeliveryRequest request = TargetDeliveryRequest.builder()
       .context(context)
       .decisioningMethod(DecisioningMethod.ON_DEVICE)
       .execute(executeRequest)
       .build();
   
       TargetDeliveryResponse response = targetClient.getOffers(request);
     logger.debug("Response: ", response.getResponse().getExecute().getMboxes().get(0).getOptions().get(0).getContent());
   } catch (Exception exception) {
     logger.error("Something went wrong", exception);
   }
   ```

1. Herzie de logboeken in uw terminal om te verifiëren dat uw inhoud wordt geleverd en dat het via het regelaarsfeit op uw server werd geleverd. De `LD.DeciscionProvider` -object wordt uitgevoerd wanneer de kwalificatie van de activiteit en de beslissing op het apparaat zijn bepaald op basis van de artefact van de regels. Bovendien is het door de `content`moet u `<div>test</div>` of u hebt echter besloten dat de reactie moet zijn wanneer u de testactiviteit maakt.

   **Uitvoer van logger**

   ```text {line-numbers="true"}
   AT: LD.DecisionProvider {...}
   AT: Response received {...}
   Response:  <div>test</div>
   ```

## Inspect verzendt meldingsfouten

Wanneer het gebruiken van Beslissing op apparaat, worden de berichten verzonden automatisch voor getOffers voert verzoeken uit. Deze verzoeken worden op de achtergrond ongemerkt verzonden. Om het even welke fouten kunnen worden geïnspecteerd door zich op een geroepen gebeurtenis te abonneren `sendNotificationError`. Hier is een codevoorbeeld dat toont hoe te aan berichtfouten in te tekenen gebruikend Node.js SDK.

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
let client;

function onSendNotificationError({ notification, error }) {
  console.log(
    `There was an error when sending a notification: ${error.message}`
  );
  console.log(`Notification Payload: ${JSON.stringify(notification, null, 2)}`);
}

async function targetClientReady() {
  const request = {
    context: { channel: "web" },
    execute: {
      mboxes: [{
        name: "a1-serverside-ab",
        index: 1
      }]
    }
  };
  const targetResponse = await client.getOffers({ request });
}

client = TargetClient.create({
  events: {
    clientReady: targetClientReady,
    sendNotificationError: onSendNotificationError
  }
});
```

## Algemene scenario&#39;s voor probleemoplossing

Controleer dit [ondersteunde functies](supported-features.md) for [!UICONTROL on-device decisioning] wanneer u problemen tegenkomt.

### Beslissingsactiviteiten op het apparaat die niet worden uitgevoerd vanwege niet-ondersteund publiek of activiteit

Een veel voorkomend probleem is [!UICONTROL on-device decisioning] activiteiten die niet worden uitgevoerd vanwege het gebruikte publiek of het type activiteit dat niet wordt ondersteund.

(1) Gebruikend de logboekoutput, herzie de ingangen in het spoorbezit in uw reactievoorwerp. Identificeer specifiek het campagnebezit:

**Uitvoer overtrekken**

```text {line-numbers="true"}
  "execute": {
  "mboxes": [
    {
      "name": "your-mbox-name",
      "index": 0,
      "trace": {
        "clientCode": "your-client-code",
        ...
        "campaigns": [],
        ...
      }
    }
```

Je zult zien dat de activiteit waarvoor je in aanmerking probeert te komen, zich niet in de `campaigns` eigenschap omdat het publiek- of activiteitstype niet wordt ondersteund. Als de activiteit onder `campaigns` eigenschap, is uw uitgave niet te wijten aan een niet-ondersteund publiek- of activiteitstype.

(2) Zoek bovendien de `rules.json` bestand door naar het `trace` > `artifact` > `artifactLocation` in de loggeruitvoer. U ziet dat uw activiteit ontbreekt in het gedeelte `rules` > `mboxes` eigenschap:

**Uitvoer van logger**

```text {line-numbers="true"}
 ...
 rules: {
   mboxes: { },
   views: { }
 }
```

Ten slotte navigeert u naar de[!DNL Target]UI en zoek de activiteit in kwestie: [experience.adobe.com/target](https://experience.adobe.com/target)

Bekijk de regels die in het publiek worden gebruikt en zorg ervoor dat u alleen de hierboven vermelde regels gebruikt die worden ondersteund. Bovendien, zorg ervoor dat het activiteitstype of A/B of XT is.

![alternatieve afbeelding](assets/asset-target-audience-ui.png)

### Beslissingsactiviteiten op het apparaat die niet worden uitgevoerd vanwege een niet-gekwalificeerd publiek

Als een beslissingsactiviteit op het apparaat niet wordt uitgevoerd, maar u hebt geverifieerd dat het bestand rules.json de activiteit bevat, voert u de volgende stappen uit:

(1) Zorg ervoor dat de box die u uitvoert in uw toepassing dezelfde is als de activiteit:

>[!BEGINTABS]

>[!TAB rule.json]

```text {line-numbers="true"}
 ...
 rules: {
   mboxes: {
    target-only-node-sdk-mbox: [{ // this mbox name must match the mbox in your request
      ...
    }]
   }
 ...
```

>[!TAB Node.js SDK]

```js {line-numbers="true"}
 const request = {
   trace: {
     authorizationToken: '2dfc1dce-1e58-4e05-bbd6-a6725893d4d6'
   },
   execute: {
     mboxes: [{
       address: getAddress(req),
       name: "target-only-node-sdk-mbox-two" // this mbox name must match the mbox the activity is using
     }]
   }};
```

>[!TAB Java SDK]

```js {line-numbers="true"}
Context context = new Context()
  .channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("target-only-node-sdk-mbox-two")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .decisioningMethod(DecisioningMethod.ON_DEVICE)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse response = targetClient.getOffers(request);
```

>[!ENDTABS]

(2) Zorg ervoor dat u gekwalificeerd bent voor het publiek voor uw activiteit door het `matchedRuleConditions` of `unmatchedRuleConditions` eigenschap van uw traceringsuitvoer:

**Uitvoer overtrekken**

```text {line-numbers="true"}
...
},
"campaignId": 368564,
"campaignType": "landing",
"matchedSegmentIds": [],
"unmatchedSegmentIds": [
  6188838
      ],
      "matchedRuleConditions": [],
          "unmatchedRuleConditions": [
            {
              "in": [
                "true",
                {
                  "var": "mbox.auth_lc"
                }
              ]
            }
          ]
    ...
```

Als u niet-afgedekte regelvoorwaarden hebt, bent u niet gekwalificeerd voor de activiteit en wordt de activiteit dus niet uitgevoerd. Bekijk de regels in uw publiek om te zien waarom u niet in aanmerking komt.

### Beslissingsactiviteit op het apparaat wordt niet uitgevoerd, maar de reden is onduidelijk

Het kan niet gemakkelijk duidelijk zijn waarom een beslissingsactiviteit op het apparaat niet wordt uitgevoerd. In dit geval voert u de volgende stappen uit om het probleem te identificeren:

(1) Lees door de logger spooroutput in uw console en identificeer het artefact bezit, dat aan het volgende gelijkaardig zal kijken:

**Uitvoer overtrekken**

```text {line-numbers="true"}
...
      "artifact": {
          "artifactLocation": "https://assets.adobetarget.com/your-client-code/production/v1/rules.json",
          "pollingInterval": 300000,
          "pollingHalted": false,
          "artifactVersion": "1.0.0",
          "artifactRetrievalCount": 3,
          "artifactLastRetrieved": "2020-10-16T00:56:27.596Z",
          "clientCode": "adobeinterikleisch",
          "environment": "production"
        },
...
```

Kijk naar de `artifactLastRetrieved` datum van het artefact en zorg ervoor dat u de recentste hebt `rules.json` naar uw app gedownload bestand.

(2) Zoek de `evaluatedCampaignTargets` eigenschap in uw logboekuitvoer:

**Uitvoer van logger**

```text {line-numbers="true"}
...
  "evaluatedCampaignTargets": [
      {
        "context": {
          "current_timestamp": 1602812599608,
          "current_time": "0143",
          "current_day": 5,
          "user": {
            "browserType": "unknown",
            "platform": "Unknown",
            "locale": "en",
            "browserVersion": -1
          },
          "page": {
            "url": "localhost:3000/",
            "path": "/",
            "query": "",
            "fragment": "",
            "subdomain": "",
            "domain": "3000",
            "topLevelDomain": "",
            "url_lc": "localhost:3000/",
            "path_lc": "/",
            "query_lc": "",
            "fragment_lc": "",
            "subdomain_lc": "",
            "domain_lc": "3000",
            "topLevelDomain_lc": ""
          },
          "referring": {
            "url": "localhost:3000/",
            "path": "/",
            "query": "",
            "fragment": "",
            "subdomain": "",
            "domain": "3000",
            "topLevelDomain": "",
            "url_lc": "localhost:3000/",
            "path_lc": "/",
            "query_lc": "",
            "fragment_lc": "",
            "subdomain_lc": "",
            "domain_lc": "3000",
            "topLevelDomain_lc": ""
          },
          "geo": {},
          "mbox": {},
          "allocation": 23.79
        },
        "campaignId": 368564,
        "campaignType": "landing",
        "matchedSegmentIds": [],
        "unmatchedSegmentIds": [
          6188838
        ],
        "matchedRuleConditions": [],
        "unmatchedRuleConditions": [
          {
            "in": [
              "true",
              {
                "var": "mbox.auth_lc"
              }
            ]
          }
        ]
...
```

(3) De `context`, `page`, en `referring` gegevens om ervoor te zorgen dat deze gegevens op de verwachte wijze worden uitgevoerd, hetgeen van invloed kan zijn op de kwalificatie van de activiteit als doelgericht doel.

(4) Herzie de `campaignId` om ervoor te zorgen dat de activiteit of activiteiten die u verwacht uit te voeren, worden geëvalueerd. De `campaignId` komt overeen met de activiteit-id op het tabblad activity overview in het dialoogvenster[!DNL Target]UI:

![alternatieve afbeelding](assets/asset-activity-id-target-ui.png)

(5) De `matchedRuleConditions` en `unmatchedRuleConditions` om problemen te identificeren waarvoor de publieksregels voor een bepaalde activiteit in aanmerking komen.

(6) Controleer de meest recente `rules.json` om te controleren of de activiteit of activiteiten die u lokaal wilt uitvoeren, zijn opgenomen. Naar de locatie wordt in stap 1 hierboven verwezen.

(7) Zorg ervoor dat u dezelfde mbox-namen gebruikt in uw aanvraag en activiteiten.

(8) Zorg ervoor dat u de ondersteunde publieksregels en ondersteunde activiteitstypen gebruikt.

### Een servervraag wordt gemaakt alhoewel de activiteitenopstelling onder een brievenbus &quot;op Apparaatbesluit in aanmerking komend&quot;in het[!DNL Target]gebruikersinterface

Er zijn een paar redenen waarom een servervraag wordt gemaakt alhoewel het apparaat voor op-apparatenbesluit verkiesbaar is:

* Wanneer de box die wordt gebruikt voor een in aanmerking komende activiteit &quot;Op apparaat beslissend&quot; ook wordt gebruikt voor andere activiteiten die niet in aanmerking komen voor &quot;Op apparaat beslissende actie&quot;, wordt de box weergegeven onder de categorie `remoteMboxes` in de `rules.json` artefact. Wanneer een box onder `remoteMboxes`, alle `getOffer(s)` de vraag aan dat mbox resulteert in een servervraag.

* Als u een activiteit onder een werkruimte/eigenschap instelt en niet hetzelfde opneemt bij het configureren van de SDK, kan dit `rules.josn` van de standaardwerkruimte die moet worden gedownload. U kunt deze werkruimte onder de `remoteMboxes` sectie.
