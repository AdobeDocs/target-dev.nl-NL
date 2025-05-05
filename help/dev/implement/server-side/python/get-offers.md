---
title: getOffers() gebruiken in [!DNL Adobe Target] bij gebruik van de Python SDK
description: Leer hoe u getOffers() gebruikt om een beslissing uit te voeren en een ervaring op te halen uit [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 9539b806-e070-430e-80cf-cf632ce3f207
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Voorstel ophalen (Python)

## Beschrijving

`get_offers()` wordt gebruikt om een besluit uit te voeren en een ervaring van terug te winnen [!DNL Adobe Target].


## Methode

### getOffers

```python {line-numbers="true"}
target_client_instance.get_offers(options)
```

## Parameters

De `options` dict heeft de volgende structuur:

| Naam | Type | Vereist | Standaard | Beschrijving |
| --- | --- | --- | --- | --- |
| verzoek | DeliveryRequest | Ja | Geen | Hiermee wordt voldaan aan de [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) verzoek |
| target_cookie | str | nee | Geen | [!DNL Target] koekje |
| target_location_hint | str | nee | Geen | [!DNL Target] locatiehint |
| consumer_id | str | nee | Geen | Wanneer het stitching van veelvoudige vraag, zouden verschillende consument IDs moeten worden verstrekt |
| customer_ids | list[CustomerId] | nee | Geen | Een lijst met Customer Ids in de indeling VisitorId die compatibel is met de klant |
| session_id | str | nee | Geen | Wordt gebruikt voor het koppelen van meerdere aanvragen |
| callback | aanroepbaar | nee | Geen | Als het behandelen van verzoek asynchroon, callback wordt aangehaald wanneer de reactie klaar is |
| err_callback | aanroepbaar | nee | Geen | Als het behandelen van verzoek asynchroon, foutencallback wordt aangehaald wanneer de uitzondering wordt opgeheven |

## Retourneert

Retourneert een `TargetDeliveryResponse` indien synchroon (standaard), of een `AsyncResult` als opgeroepen met een callback. `TargetDeliveryResponse` heeft de volgende structuur:

| Naam | Type | Beschrijving |
| --- | --- | --- |
| reactie | DeliveryResponse | Hiermee wordt voldaan aan de [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) reactie |
| target_cookie | dict | [!DNL Target] koekje |
| target_location_hint_cookie | dict | [!DNL Target] locatiehintcookie |
| analytics_details | list[AnalyticsResponse] | Analytische lading, in geval van client side Analytics gebruik |
| traceren | list[dict] | Samengevoegde spoorgegevens voor alle verzoekdozen/meningen |
| response_tokens | list[dict] | Een lijst met &#x200B;[Reactiepunten](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=nl-NL) |
| meta | dict | Aanvullende beslissingsmetagegevens voor gebruik met apparaatbesluitvorming |

`target_cookie` en `target_location_hint_cookie` objecten die worden gebruikt voor het doorgeven van gegevens naar de browser, hebben de volgende structuur:

| Naam | Type | Beschrijving |
| --- | --- | --- |
| name | str | Naam cookie |
| value | alle | Cookie-waarde, de waarde wordt omgezet in tekenreeks |
| max_age | int | De `max_age option` is een gemak voor het plaatsen verloopt met betrekking tot de huidige tijd in seconden |

De `meta` Het object dat wordt gebruikt om de status van de doelreactie aan te geven, heeft de volgende structuur:

| Naam | Type | Beschrijving |
| --- | --- | --- |
| beslissings_methode | str | Welke beslissingsmethode is gebruikt: op apparaat of op de server |
| remote_mboxes | list`[str]` | Wanneer beslissingsmethode is `on-device`Er wordt een array met namen van selectievakjes gegeven die niet volledig op het apparaat konden worden vastgesteld. Met andere woorden: [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) verzoek is nodig. |
| remote_views | list`[str]` | Wanneer de beslissingsmethode op apparaat is, wordt een array met weergavenamen gegeven die niet volledig op het apparaat konden worden vastgesteld. Met andere woorden: [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) verzoek is nodig. |

## Voorbeeld

### Python

```python {line-numbers="true"}
def client_ready_callback():
    context = Context(channel=ChannelType.WEB)
    mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_offers_options = {
      "request": delivery_request
    }

    target_delivery_response = target_client.get_offers(get_offers_options)


client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
