---
title: Abonneren op gebeurtenissen in het dialoogvenster [!DNL Adobe Target] Node.js SDK
description: Leer hoe u zich abonneert op verschillende gebeurtenissen die plaatsvinden in de Node.js SDK met de [!UICONTROL OnDeviceDecisioningHandler] object.
feature: APIs/SDKs
exl-id: 40c53840-a560-4819-ae04-f527c36b22fe
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# SDK-gebeurtenissen (Node.js)

## Beschrijving

Wanneer [initialiseren SDK](initialize-sdk.md)de `options.events` -object is een optioneel object met gebeurtenisnaamtoetsen en callback-functiewaarden. Het kan worden gebruikt om aan diverse gebeurtenissen in te tekenen die binnen SDK voorkomen. Bijvoorbeeld `clientReady` De gebeurtenis kan met een callback functie worden gebruikt die zal worden aangehaald wanneer SDK klaar voor methodevraag is.

Wanneer de callback-functie wordt aangeroepen, wordt een gebeurtenisobject doorgegeven. Elke gebeurtenis heeft een `type` komt overeen met de gebeurtenisnaam. Sommige gebeurtenissen bevatten aanvullende eigenschappen met relevante informatie.

## Gebeurtenissen

| Naam gebeurtenis (type) | Beschrijving | Aanvullende gebeurteniseigenschappen |
| --- | --- | --- |
| clientReady | Wordt verzonden wanneer het artefact is gedownload en de SDK gereed is voor `getOffers` oproepen. Aanbevolen bij gebruik van de beslissingsmethode op het apparaat. |
| artifactDownloadSuccceeded | Wordt telkens verzonden wanneer een nieuw artefact wordt gedownload. | artifactPayload, artifactLocation |
| artifactDownloadFailed | Wordt telkens verzonden wanneer een artefact niet kan worden gedownload. | artifactLocation, error |

## Voorbeeld

### Node.js

```js {line-numbers="true"}
const targetClient = TargetClient.create({
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device",
    events: {
        clientReady: onTargetClientReady,
        artifactDownloadSucceeded: onArtifactDownloadSucceeded,
        artifactDownloadFailed: onArtifactDownloadFailed
    }
});

function onTargetClientReady() {
    // make getOffers requests
    targetClient.getOffers({...})            
}

function onArtifactDownloadSucceeded(event) {
    console.log(`The artifact was successfully downloaded from '${event.artifactLocation}'`);
    // optionally do something with event.artifactPayload, like persist it
}

function onArtifactDownloadFailed(event) {
    console.log(`The artifact failed to download from '${event.artifactLocation}' with the following error message: ${event.error.message}`);
}
```
