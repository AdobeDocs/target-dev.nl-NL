---
title: getAttributes gebruiken in [!DNL Adobe Target] met de Java SDK
description: Leer hoe u getAttributes() kunt gebruiken om experimenten en persoonlijke ervaringen op te halen uit [!DNL Target] en extraheren, kenmerkwaarden.
feature: APIs/SDKs
exl-id: e493e1b9-7180-4a7c-b98d-be84cc3a57c3
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Kenmerken ophalen (Java)

## Beschrijving

`getAttributes()` wordt gebruikt om experimenten en gepersonaliseerde ervaringen van te halen [!DNL Target] en extraheren, kenmerkwaarden.

## Methode

### getAttributes

```javascript {line-numbers="true"}
Attributes TargetClient.getAttributes(TargetDeliveryRequest targetRequest, String ...mboxes)
```

## Parameters

| Naam | Type | Vereist | Standaard | Beschrijving |
| --- | --- | --- | --- | --- |
| targetRequest | TargetDeliveryRequest | Ja | Geen | Dezelfde doelaanvraag als gebruikt voor [&#x200B; ophalen](get-offers.md) |
| mboxNames | var-args-array | Nee | Geen | Een var-args-array van mbox-namen |


## Resultaat

An `Attributes` object wordt geretourneerd van `TargetClient.getAttributes()` met de volgende methoden:

| Naam | Type | Beschrijving |
| --- | --- | --- |
| getBoolean(mboxName, key) | Boolean | Hiermee wordt de waarde voor een opgegeven naam en kenmerksleutel geretourneerd |
| getString(mboxName, key) | String | Hiermee wordt de waarde voor een opgegeven naam en kenmerksleutel geretourneerd |
| getInteger(mboxName, key) | Geheel | Hiermee wordt de waarde voor een opgegeven naam en kenmerksleutel geretourneerd |
| getDouble(mboxName, key) | Dubbel | Hiermee wordt de waarde voor een opgegeven naam en kenmerksleutel geretourneerd |
| toMboxMap(mboxName) | Kaart | Hiermee wordt een eenvoudige map met sleutelwaardeparen geretourneerd |
| getResponse() | TargetDeliveryResponse | Retourneert het reactieobject dat normaal door getOffers wordt geretourneerd |

## Voorbeeld

### Java

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .build();

Attributes offerAttributes = targetJavaClient.getAttributes(targetDeliveryRequest, "demo-engineering-flags");

//returns just the value of searchProviderId from the mbox offer
String searchProviderId = offerAttributes.getString("demo-engineering-flags", "searchProviderId");

//returns a simple Map representing the mbox offer
Map<String, Object> engineeringFlags = offerAttributes.toMboxMap("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

String assetUrl = "http://" + engineeringFlags.cdnHostname + "/path/to/asset";
```
