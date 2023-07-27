---
title: Hoe te om asynchrone verzoeken in te gebruiken [!DNL Adobe Target] Python SDK
description: Meer informatie [!DNL Target] Python SDK ondersteunt asynchrone verzoeken, waardoor de effectieve doeltijd tot nul kan worden teruggebracht.
feature: APIs/SDKs
exl-id: fafb9e28-5ac5-41c1-8e7f-f40550b6749f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Kenmerken ophalen (Python)

## Beschrijving

`get_attributes()` wordt gebruikt om experimenten en gepersonaliseerde ervaringen van te halen [!DNL Target] en extraheren, kenmerkwaarden.


## Methode

### getAttributes

```python {line-numbers="true"}
target_client_instance.get_attributes(mbox_names, options)
```

## Parameters

| Naam | Type | Vereist | Standaard | Beschrijving |
| --- | --- | --- | --- | --- |
| mbox_names | list[str] | Ja | Geen | Een lijst met veldnamen |
| opties | dict | Nee | Geen | Dezelfde opties als worden gebruikt voor [Voorstel ophalen](get-offers.md) |

## AttributesProvider

De `AttributesProvider` geretourneerd door `target_client.get_attributes()` heeft de volgende methoden:

| Methode | Retourtype | Beschrijving |
| --- | --- | --- |
| get_value(mbox_name, key) | alle | Hiermee wordt de waarde voor een opgegeven naam en kenmerksleutel geretourneerd |
| as_object(mbox_name) | dict | Hiermee wordt een eenvoudig json-object met sleutelwaardeparen geretourneerd |
| get_response() | [TargetDeliveryResponse](https://github.com/adobe/target-python-sdk/blob/main/target_python_sdk/types/target_delivery_response.py) | Retourneert het reactieobject dat normaal wordt geretourneerd door `get_offers` |

## Voorbeeld

### Python

```python {line-numbers="true"}
def client_ready_callback():
    context = Context(channel=ChannelType.WEB)
    mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_attributes_options = {
      "request": delivery_request
    }

    attributes_provider = target_client.get_attributes(["demo-engineering-flags"], get_attributes_options)
    # returns just the value of searchProviderId from the demo-engineering-flags mbox offer
    search_provider_id = attributes_provider.get_value("demo-engineering-flags", "searchProviderId")

    # returns a simple dict object representing the demo-engineering-flags mbox offer
    engineering_flags = attributes_provider.as_object("demo-engineering-flags")
    """  the value of engineeringFlags looks like this
        {
            "cdnHostname": "cdn.cloud.corp.net",
            "searchProviderId": 143,
            "hasLegacyAccess": false
        }
    """

    asset_url = "http://{}/path/to/asset".format(engineering_flags.get("cdnHostname"))


client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
