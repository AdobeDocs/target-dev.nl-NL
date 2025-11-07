---
title: Abonneren aan gebeurtenissen in  [!DNL Adobe Target]  Node.js SDK
description: Leer hoe u zich abonneert op verschillende gebeurtenissen die plaatsvinden in de SDK Node.js met behulp van het [!UICONTROL OnDeviceDecisioningHandler] -object.
feature: APIs/SDKs
exl-id: 40c53840-a560-4819-ae04-f527c36b22fe
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# SDK Events (Node.js)

## Beschrijving

Wanneer [ het initialiseren van SDK ](initialize-sdk.md), is het `options.events` voorwerp een facultatief voorwerp met de sleutels van de gebeurtenisnaam en callback functiewaarden. Deze kan worden gebruikt om een abonnement te nemen op verschillende gebeurtenissen die plaatsvinden in de SDK. De gebeurtenis `clientReady` kan bijvoorbeeld worden gebruikt met een callback-functie die wordt aangeroepen wanneer de SDK gereed is voor methodeaanroepen.

Wanneer de callback-functie wordt aangeroepen, wordt een gebeurtenisobject doorgegeven. Elke gebeurtenis heeft een `type` die overeenkomt met de naam van de gebeurtenis. Sommige gebeurtenissen bevatten aanvullende eigenschappen met relevante informatie.

## Gebeurtenissen

| Naam gebeurtenis (type) | Beschrijving | Aanvullende gebeurteniseigenschappen |
| --- | --- | --- |
| clientReady | Wordt verzonden wanneer het artefact is gedownload en de SDK gereed is voor `getOffers` -aanroepen. Aanbevolen bij gebruik van de beslissingsmethode op het apparaat. |  |
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
