---
title: Abonneren op gebeurtenissen in het dialoogvenster [!DNL Adobe Target] .NET SDK
description: Leer hoe te aan diverse gebeurtenissen intekenen die binnen .NET SDK voorkomen gebruikend [!UICONTROL OnDeviceDecisioningHandler] object.
feature: APIs/SDKs
exl-id: 7578033f-3de5-4d13-9739-46ad1269ec5f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# SDK-gebeurtenissen (.NET)

## Beschrijving

Wanneer [initialiseren SDK](initialize-sdk.md), een facultatieve `OnDeviceDecisioningReady` de afgevaardigde kan op de `TargetClientConfig` -object, dat wordt aangeroepen wanneer de SDK gereed is voor aanroepen van methoden op het apparaat. Er zijn ook een paar andere afgevaardigden beschikbaar voor het afhandelen van de [!UICONTROL on-device decisioning] artefactdownload.

## Gebeurtenissen

De volgende afgevaardigden kunnen voor bepaalde gebeurtenissen worden gevormd:

| Naam | Argumenten | Beschrijving |
| --- | --- | --- |
| OnDeviceDecisioningReady | Geen | Wordt slechts eenmaal aangeroepen wanneer de client voor de eerste keer gereed is [!UICONTROL on-device decisioning] |
| ArtifactDownloadSuccceeded | tekenreeksinhoud van artefactbestand | Wordt telkens opgeroepen en [!UICONTROL on-device decisioning] artefact is gedownload |
| ArtifactDownloadFailed | Uitzondering | Wordt aangeroepen wanneer er een fout optreedt bij het downloaden van een [!UICONTROL on-device decisioning] artefact |

## Voorbeeld

### \.NET

```dotnet {line-numbers="true"}
var clientConfig = new TargetClientConfig.Builder("acmeclient", "1234567890@AdobeOrg")
    .SetDecisioningMethod(DecisioningMethod.OnDevice)
    .SetOnDeviceDecisioningReady(DecisioningReady)
    .SetArtifactDownloadSucceeded(artifact => Console.WriteLine("The artifact was successfully downloaded. Contents: " + artifact))
    .SetArtifactDownloadFailed(exception => Console.WriteLine("The artifact failed to download. Exception: " + exception.Message))
    .Build();

var targetClient = TargetClient.Create(clientConfig);

// ...

static void DecisioningReady()
{
    var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

    var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
        .SetExecute(new ExecuteRequest(mboxes: mboxRequests))
        .Build();

    var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
}
```
