---
title: Abonneren op gebeurtenissen in het dialoogvenster [!DNL Adobe Target] Java SDK
description: Leer hoe u zich kunt abonneren op verschillende gebeurtenissen die plaatsvinden in de Java SDK met de opdracht [!UICONTROL OnDeviceDecisioningHandler] object.
feature: APIs/SDKs
exl-id: f2d56762-6bf7-4c6b-9c14-fb20e5cfd60d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# SDK-gebeurtenissen (Java)

## Beschrijving

Wanneer [initialiseren SDK](initialize-sdk.md), een facultatieve `OnDeviceDecisioningHandler` object kan worden opgegeven op het tabblad `ClientConfig` object. Het kan worden gebruikt om aan diverse gebeurtenissen in te tekenen die binnen SDK voorkomen. Bijvoorbeeld de `onDeviceDecisioningReady` De gebeurtenis kan met een callback functie worden gebruikt die zal worden aangehaald wanneer SDK klaar voor methodevraag is.

## Gebeurtenissen

De `OnDeviceDecisioningHandler` Het object bevat de volgende callbacks, die voor bepaalde gebeurtenissen worden aangeroepen:

| Naam | Argumenten | Beschrijving |
| --- | --- | --- |
| onDeviceDecisioningReady | Geen | Wordt slechts eenmaal aangeroepen wanneer de client voor de eerste keer gereed is [!UICONTROL on-device decisioning] |
| artifactDownloadSuccceeded | byte[] inhoud van artefactbestand | Wordt telkens opgeroepen [!UICONTROL on-device decisioning] artefact is gedownload |
| artifactDownloadFailed | Uitzondering | Wordt aangeroepen wanneer er een fout optreedt bij het downloaden van een [!UICONTROL on-device decisioning] artefact |

## Voorbeeld

### SDK-gebeurtenissen

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .defaultDecisioningMethod(DecisioningMethod.ON_DEVICE)
        .onDeviceDecisioningHandler(new OnDeviceDecisioningHandler() {
            @Override
            public void onDeviceDecisioningReady() {
                // make getOffers requests
                makeTargetRequests();
            }

            @Override
            public void artifactDownloadSucceeded(byte[] artifactData) {
                System.out.println("The artifact was successfully downloaded.");
            }

            @Override
            public void artifactDownloadFailed(TargetClientException e) {
                System.out.println("The artifact failed to download.");
            }
        }).build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);


void makeTargetRequests() {
    List<MboxRequest> mboxRequests = new ArrayList<>();
    mboxRequests.add((MboxRequest) new MboxRequest().name("a1-serverside-ab").index(1));

    TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
            .context(new Context().channel(ChannelType.WEB))
            .execute(new ExecuteRequest().setMboxes(mboxRequests))
            .build();

    TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
}
```
