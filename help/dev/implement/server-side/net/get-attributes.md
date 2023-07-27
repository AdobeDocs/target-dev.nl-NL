---
title: getAttributes gebruiken in [!DNL Adobe Target] met de .NET SDK
description: Leer hoe u getAttributes() kunt gebruiken om experimenten en persoonlijke ervaringen op te halen uit [!DNL Target] en extraheren, kenmerkwaarden.
feature: APIs/SDKs
exl-id: 808da83d-3077-468b-a2ad-e35c25905f7d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Kenmerken ophalen (.NET)

## Beschrijving

`GetAttributes()` wordt gebruikt om experimenten en gepersonaliseerde ervaringen van te halen [!DNL Target] en extraheren, kenmerkwaarden.

## Methode

### getAttributes

```dotnet {line-numbers="true"}
TargetAttributes TargetClient.GetAttributes(TargetDeliveryRequest targetRequest, params string[] mboxes)
```

## Parameters

| Naam | Type | Vereist | Standaard | Beschrijving |
| --- | --- | --- | --- | --- |
| targetRequest | TargetDeliveryRequest | Nee | null | Hetzelfde [!DNL Target] verzoek zoals gebruikt voor [&#x200B; ophalen](get-offers.md) |
| mboxNames | params, tekenreeks[] | Nee | null | Een parameterarray van namen van selectievakjes |

## Resultaat

A `TargetAttributes` object wordt geretourneerd van `TargetClient.GetAttributes()` met de volgende eigenschappen en methoden:

| Eigenschap/methode | Retourtype | Beschrijving |
| --- | --- | --- |
| Antwoord | TargetDeliveryResponse | Retourneert het reactieobject dat normaal wordt geretourneerd door [Voorstel ophalen](get-offers.md) |
| ToDictionary | IReadOnlyDictionary | Hiermee wordt een woordenboek van woordenboeken geretourneerd met sleutelwaardeparen gegroepeerd op veldnamen |
| ToMboxDictionary(mboxName) | IReadOnlyDictionary | Hiermee wordt een woordenboek met sleutelwaardeparen voor het opgegeven vak geretourneerd |
| GetBoolean(mboxName, key, defaultValue) | bool | Hiermee wordt de waarde voor een opgegeven naam en kenmerksleutel geretourneerd |
| GetString(mboxName, key, defaultValue) | string | Hiermee wordt de waarde voor een opgegeven naam en kenmerksleutel geretourneerd |
| GetInteger(boxName, key, defaultValue) | int | Hiermee wordt de waarde voor een opgegeven naam en kenmerksleutel geretourneerd |
| GetDouble(mboxName, key, defaultValue) | double | Hiermee wordt de waarde voor een opgegeven naam en kenmerksleutel geretourneerd |
| GetValue(mboxName, key, defaultValue) | T | Hiermee wordt de waarde voor een opgegeven naam en kenmerksleutel geretourneerd |

## Voorbeeld

### \.NET

```dotnet {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

var targetClient = TargetClient.Create(targetClientConfig);

var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .Build();

var offerAttributes = targetClient.GetAttributes(targetDeliveryRequest, "demo-engineering-flags");

//returns just the value of searchProviderId from the mbox offer
var searchProviderId = offerAttributes.GetString("demo-engineering-flags", "searchProviderId");

//returns a simple Dictionary representing the mbox offer
var engineeringFlags = offerAttributes.ToMboxDictionary("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

var assetUrl = $"http://{engineeringFlags["cdnHostname"]}/path/to/asset";
```
