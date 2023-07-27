---
title: Gebruiken [!UICONTROL getOffers()] in [!DNL Adobe Target] bij gebruik van de Node.js SDK
description: Leren gebruiken [!UICONTROL getOffers()] om een beslissing uit te voeren en een ervaring op te halen uit [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 3c4125ea-68d4-405e-9b9a-5fa832743153
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# [!UICONTROL Get Offers] (Node.js)

## Beschrijving

`[!UICONTROL getOffers()]` wordt gebruikt om een besluit uit te voeren en een ervaring van terug te winnen [!DNL Adobe Target].


## Methode

### getOffers

```js {line-numbers="true"}
TargetClient.getOffers(options: Object): Promise
```

## Parameters

De `options` object heeft de volgende structuur:

| Naam | Type | Vereist | Standaard | Beschrijving |
| --- |--- | --- | --- | --- |
| Verzoek | Object | Ja | Geen | Hiermee wordt voldaan aan de [[!DNL Target] Leverings-API](/help/dev/implement/delivery-api/overview.md) verzoek |
| bezoekerCookie | String | Nee | Geen | CECID-cookie (VisitorId) |
| targetCookie | String | Nee | Geen | [!DNL Target] koekje |
| targetLocationHint | String | Nee | Geen | [!DNL Target] locatiehint |
| consumerId | Sting | Nee | Geen | ConsumerIds voor [!UICONTROL Analytics for Target] (A4T) stitching |
| CustomerIds | Array | Nee | Geen | Klant-id&#39;s in de indeling VisitorId die compatibel is met |
| sessionId | String | Nee | Geen | Wordt gebruikt voor het koppelen van meerdere [!DNL Target] verzoeken |
| bezoeker | Object | Nee | new VisitorId | Een externe VisitorId-instantie leveren |

## beloften

`Promise` teruggekeerd heeft de volgende structuur:

| Naam | Type | Beschrijving |
| --- | --- | --- |
| verzoek | Object | [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) verzoek |
| reactie | Object | [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) reactie |
| bezoekerState | Object | Object dat moet worden doorgegeven aan de Bezoeker-API `getInstance()` |
| targetCookie | Object | [!DNL Target] koekje |
| targetLocationHintCookie | Object | [!DNL Target] locatiehintcookie |
| analyticsDetails | Array | Analyselading, in geval van client-side Analytics-gebruik |
| responseTokens | Array | Een lijst van [Reactietokens](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?). |
| traceren | Array | Samengevoegde spoorgegevens voor alle verzoekdozen/meningen |
| status | Object | Een object dat de status van het antwoord bevat. |
| determinoningMethod | String | Bepaalt welke beslissingsmethode moet worden gebruikt ([op apparaat](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), server-kant, hybride) |

`targetCookie` en `targetLocationHintCookie` objecten die worden gebruikt voor het doorgeven van gegevens naar de browser, hebben de volgende structuur:

| Naam | Type | Beschrijving |
| --- | --- | --- |
| name | String | Naam cookie |
| value | Alle | Cookie-waarde, de tekenreeks wordt omgezet |
| maxAge | Getal | De `maxAge` optie is een gemak voor het plaatsen verloopt met betrekking tot de huidige tijd in seconden |

De `status` Het object dat wordt gebruikt om de status van de doelreactie aan te geven, heeft de volgende structuur:

| Naam | Type | Beschrijving |
| --- | --- | --- |
| status | Getal | HTTP-statuscode |
| message | String | Een bericht over de reactie. Het kan bijvoorbeeld aangeven of een beslissing over het antwoord is genomen [op apparaat](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md) of op de server |
| remoteMboxes | Array | Wanneer beslissingsmethode is `on-device`Er wordt een array met namen van selectievakjes gegeven die niet volledig op het apparaat konden worden vastgesteld. Met andere woorden: [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) verzoek is nodig. |

## Voorbeeld

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

const request = {
    context: {channel: "web"},
    execute: {
        mboxes: [{
            name: "a1-serverside-ab",
            index: 1
        }]
}};

const response = await targetClient.getOffers({ request });
```
