---
title: Hoe te om asynchrone verzoeken in te gebruiken [!DNL Adobe Target] Python SDK
description: Meer informatie [!DNL Target] Python SDK ondersteunt asynchrone verzoeken, waardoor de effectieve doeltijd tot nul kan worden teruggebracht.
feature: APIs/SDKs
exl-id: 44ab74e5-3c1a-49cf-9fff-fe523b0c2592
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Asynchrone verzoeken (Python)

## Beschrijving

Een voordeel van integratie aan de serverzijde is dat u de enorme bandbreedte en computerbronnen die beschikbaar zijn aan de serverzijde kunt benutten door parallellisme te gebruiken. [!DNL Target] Python SDK ondersteunt asynchrone verzoeken, waardoor de effectieve doeltijd tot nul kan worden teruggebracht.

## Ondersteunde methoden

### Python

```python {line-numbers="true"}
get_offers(options)
send_notifications(options)
get_attributes(mbox_names, options)
```

## Voorbeeld

Een voorbeeldtoepassing waarin de `asyncio` De async/wachttijd van de module in Python 3.9+ zou als volgt kunnen kijken:

### Python

```python {line-numbers="true"}
async def execute_mboxes(self, mboxes):
    context = Context(channel=ChannelType.WEB)
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_offers_options = {
      "request": delivery_request
    }
    return await asyncio.to_thread(target_client.get_offers, get_offers_options)

async def get_target_delivery_response(mboxes):
    target_delivery_response = await execute_mboxes(mboxes)
    response = Response(target_delivery_response.get("response").to_str(), status=200, mimetype='application/json')
    return response

mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
return asyncio.run(get_target_delivery_response(mboxes)
```

In dit voorbeeld wordt aangenomen dat u Python 3.9+ gebruikt. Als u een oudere versie van Python gebruikt, kunt u nog steeds asynchrone verzoeken verzenden door `options.callback` tot `get_offers`. Bekijk de voorbeeldtoepassing Flask voor meer informatie over asynchrone uitvoering met callbacks of async/await. [hier](https://github.com/adobe/target-python-sdk/blob/main/samples/app.py).
