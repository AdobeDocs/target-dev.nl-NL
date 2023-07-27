---
title: Initialiseer Node.js SDK gebruikend creeer methode
description: Leer hoe u de methode create gebruikt om de Node.js SDK te initialiseren en het [!DNL Target] cliënt om vraag te maken aan [!DNL Adobe Target] voor experimenten en persoonlijke ervaringen.
feature: APIs/SDKs
exl-id: 71516e44-508a-4d8d-9f2b-7c54243e9c60
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# De SDK van Node.js initialiseren

## Beschrijving

Gebruik de `create` om de Node.js SDK te initialiseren en het [!UICONTROL Target] cliënt om vraag te maken aan [!DNL Adobe Target] voor experimenten en persoonlijke ervaringen.

## Methode

**maken**

```js {line-numbers="true"}
TargetClient.create(options: Object): TargetClient
```

## Parameters

`options` heeft de volgende structuur:

| Naam | Type | Vereist | Standaard | Beschrijving |
| --- | --- | --- | --- | --- |
| client | String | Ja | Geen | [!UICONTROL Adobe Target Client ID] |
| organisationId | String | Ja | Geen | [!UICONTROL Experience Cloud Organization ID] |
| milieu | String | Nee | productie | Naam doelomgeving. In de [!DNL Target] UI [!UICONTROL Administration] > [!UICONTROL Environments]. |
| timeout | Getal | Nee | 3000 | Time-out in milliseconden |
| serverDomain | String | Nee | `*client*.tt.omtrdc.net` | Overschrijft de standaardhostnaam |
| beveiligen | Boolean | Nee | true | Ongedaan maken om HTTP-schema af te dwingen |
| registreerapparaat | Object | Nee | NOOP-logger | Hiermee vervangt u de standaard NOOP-logboekregistratie |
| targetLocationHint | String | Nee | Geen | Tip voor doellocatie |
| fetchApi | -functie | Nee | global.fetch of window.fetch | [ophalen](https://fetch.spec.whatwg.org/) wordt gebruikt door de SDK voor http-verzoeken. Door gebrek wordt de knoop-halen of browser implementatie van halen gebruikt. Maar er kan een alternatieve implementatie worden geboden met behulp van `fetchApi` |
| propertyToken | String | Nee | Geen | **Token doeleigenschap**. Indien hier opgegeven, alles `getOffers` de vraag zal deze waarde gebruiken. **Voor het bepalen van het apparaat**, downloadt de SDK alleen het artefact dat de gekwalificeerde activiteiten bevat voor de eigenschap token die is ingesteld in `propertyToken` |
| determinoningMethod | String | Nee | server-kant | Bepaalt welke beslissingsmethode moet worden gebruikt ([op apparaat](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), server-kant, hybride) |
| pollingInterval | Getal | Nee | 300000 (5 minuten) | Opiniepeilingsinterval voor de [Artefact van regel voor apparaatbeslissingen](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) (in milliseconden) |
| artifactLocation | String | Nee | Geen | Een volledig gekwalificeerde URL naar de [Artefact van regel voor apparaatbeslissingen](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Hiermee overschrijft u de intern bepaalde locatie. |
| artifactPayload | Object | Nee | Geen | De JSON-lading van de [Artefact van regel voor apparaatbeslissingen](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Indien opgegeven, wordt deze gebruikt in plaats van een aanvraag via een URL in te dienen. |
| [gebeurtenissen](sdk-events.md) | Object&lt;string function=&quot;&quot;> | Nee | Geen | Een optioneel object met gebeurtenisnaamtoetsen en callback-functiewaarden |
| telemetryEnabled | Boolean | Nee | true | Als deze optie is ingeschakeld, verzamelt Adobe het gebruik van de SDK-functie en de telemetriegegevens voor de prestaties. Persoonlijke gegevens worden niet verzameld. |

## Voorbeeld

### Node.js

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    events: {clientReady: targetClientReady }
};

const targetClient = TargetClient.create(CONFIG);

function targetClientReady() {
    // make calls to Adobe Target
}
```
