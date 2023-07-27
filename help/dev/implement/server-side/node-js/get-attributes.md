---
title: Hoe te om asynchrone verzoeken in te gebruiken [!DNL Adobe Target] Node.js SDK
description: Meer informatie [!DNL Target] Node.js SDK steunt asynchrone verzoeken, die de efficiënte doeltijd tot nul kunnen verminderen.
feature: APIs/SDKs
exl-id: aa06f3ca-7d2a-4334-8092-730a8705dfb0
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Kenmerken ophalen (Node.js)

## Beschrijving

`[!UICONTROL getAttributes()]` wordt gebruikt om experimenten en gepersonaliseerde ervaringen van te halen [!DNL Target] en extraheren, kenmerkwaarden.

## Methode

### getAttributes

```js {line-numbers="true"}
TargetClient.getAttributes(mboxNames: Array, options: Object): Promise
```

## Parameters

| Naam | Type | Vereist | Standaard |
| --- | --- | --- |--- |
| mboxNames | Array | Ja | Geen |
| opties | Object | Nee | Geen |

## beloften

De `Promise` geretourneerd door `TargetClient.getAttributes()` Hiermee wordt een object met de volgende methoden omgezet:

| Methode | Retourtype | Beschrijving |
| --- | --- | --- |
| getValue(mboxName, key) | Alle | Hiermee wordt de waarde voor een opgegeven naam en kenmerksleutel geretourneerd |
| asObject(mboxName) | Object | Hiermee wordt een eenvoudig json-object met sleutelwaardeparen geretourneerd |
| getResponse() | [getOffers Response](https://github.com/jasonwaters/target-nodejs-sdk#targetclientgetoffers) | Retourneert het reactieobject dat normaal wordt geretourneerd door `getOffers` |

## Voorbeeld

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);
const offerAttributes = await targetClient.getAttributes(["demo-engineering-flags"]);


//returns just the value of searchProviderId from the mbox offer
const searchProviderId = offerAttributes.getValue("demo-engineering-flags", "searchProviderId");

//returns a simple JSON object representing the mbox offer
const engineeringFlags = offerAttributes.asObject("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

const assetUrl = `http://${engineeringFlags.cdnHostname}/path/to/asset`;
```
