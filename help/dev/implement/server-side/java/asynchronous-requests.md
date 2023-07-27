---
title: Hoe te om asynchrone verzoeken in te gebruiken [!DNL Adobe Target] Java SDK
description: Meer informatie [!DNL Target] Java SDK ondersteunt asynchrone aanvragen, waardoor de effectieve doeltijd tot nul kan worden teruggebracht.
feature: APIs/SDKs
exl-id: e11f8d16-76f6-4d39-822a-34a1cf7f623f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Asynchrone verzoeken (Java)

## Beschrijving

Een voordeel van integratie aan de serverzijde is dat u de enorme bandbreedte en computerbronnen die beschikbaar zijn aan de serverzijde kunt benutten door parallellisme te gebruiken. [!DNL Target] Java SDK ondersteunt asynchrone aanvragen, waardoor de effectieve doeltijd tot nul kan worden teruggebracht.

## Ondersteunde methoden

### Methoden

```javascript {line-numbers="true"}
CompletableFuture<TargetDeliveryResponse> getOffersAsync(TargetDeliveryRequest request);
CompletableFuture<ResponseStatus> sendNotificationsAsync(TargetDeliveryRequest request);
CompletableFuture<Attributes> getAttributesAsync(TargetDeliveryRequest targetRequest, String ...mboxes);
```

## Voorbeeld

Een monster `Spring` De toepassingscontroller kan er als volgt uitzien:

### Voorbeeldecontrole

```javascript {line-numbers="true"}
@RestController
public class TargetRestController {

    @Autowired
    private TargetClient targetJavaClient;

    @GetMapping("/mboxTargetOnlyAsync")
        public TargetDeliveryResponse mboxTargetOnlyAsync(
                @RequestParam(name = "mbox", defaultValue = "server-side-mbox") String mbox,
                HttpServletRequest request, HttpServletResponse response) {
            ExecuteRequest executeRequest = new ExecuteRequest()
                    .mboxes(getMboxRequests(mbox));

            TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
                    .context(getContext(request))
                    .execute(executeRequest)
                    .cookies(getTargetCookies(request.getCookies()))
                    .build();
            CompletableFuture<TargetDeliveryResponse> targetResponseAsync =
                    targetJavaClient.getOffersAsync(targetDeliveryRequest);
            targetResponseAsync.thenAccept(tr -> setCookies(tr.getCookies(), response));
            simulateIO();
            TargetDeliveryResponse targetResponse = targetResponseAsync.join();
            return targetResponse;
        }

    /**
     * Function for simulating network calls like other microservices and database calls
     */
    private void simulateIO() {
        try {
            Thread.sleep(200L);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

}
```

In dit voorbeeld wordt ervan uitgegaan dat u [geïnitialiseerd de SDK](initialize-sdk.md) als boerenboon en [Hulpprogrammamethoden](utility-methods.md) beschikbaar.

De [!DNL Target] aanvraag wordt gestart voordat `simulateIO` en tegen de tijd dat het doelresultaat wordt uitgevoerd zou ook klaar moeten zijn. Zelfs als dat niet het geval is, zult u in de meeste gevallen aanzienlijke besparingen hebben.
