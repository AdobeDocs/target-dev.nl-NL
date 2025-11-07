---
title: Verstuur vertoning of klik berichten aan  [!DNL Adobe Target]  gebruikend Python SDK
description: Leer hoe te om sendNotifications () te gebruiken om vertoning te verzenden of berichten aan  [!DNL Adobe Target]  voor meting en het melden te klikken.
feature: APIs/SDKs
exl-id: 03827b18-a546-4ec8-8762-391fcb3ac435
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Meldingen verzenden (Python)

## Beschrijving

`send_notifications()` wordt gebruikt om weergave- of klikmeldingen voor meting en rapportage naar [!DNL Adobe Target] te verzenden.

>[!NOTE]
>
>Wanneer een `execute` -object met vereiste parameters zich in het verzoek zelf bevindt, wordt de indruk automatisch vergroot voor kwalificerende activiteiten.

De methoden van SDK die automatisch de indruk vergroten zijn:

* `get_offers()`
* `get_attributes()`

Wanneer een `prefetch` -object binnen de aanvraag wordt doorgegeven, wordt de indruk niet automatisch vergroot voor de activiteiten met vakken binnen het `prefetch` -object. `Send_notifications()` moet worden gebruikt voor vooraf ingestelde ervaringen voor het verhogen van indrukken en conversies.

## Methode

### send_notifications

```python {line-numbers="true"}
target_client.send_notifications(options)
```

## Parameters

`options` heeft de volgende structuur:

| Naam | Type | Vereist | Standaard | Beschrijving |
| --- | --- | --- | --- | --- |
| verzoek | DeliveryRequest | Ja | Geen | Komt overeen met de aanvraag [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) |
| target_cookie | str | nee | Geen | [!DNL Target] cookie |
| target_location_hint | str | nee | Geen | [!DNL Target] locatiehint |
| consumer_id | str | nee | Geen | Wanneer het stitching van veelvoudige vraag, zouden verschillende consument IDs moeten worden verstrekt |
| customer_ids | lijst [ CustomerId ] | nee | Geen | Een lijst met Customer Ids in de indeling VisitorId die compatibel is met de klant |
| session_id | str | nee | Geen | Wordt gebruikt voor het koppelen van meerdere aanvragen |
| callback | aanroepbaar | nee | Geen | Als het behandelen van verzoek asynchroon, callback wordt aangehaald wanneer de reactie klaar is |
| err_callback | aanroepbaar | nee | Geen | Als het behandelen van verzoek asynchroon, foutencallback wordt aangehaald wanneer de uitzondering wordt opgeheven |

## Retourneert

`Returns` a `TargetDeliveryResponse` indien synchroon aangeroepen (standaard), of een `AsyncResult` indien aangeroepen met een callback. `TargetDeliveryResponse` heeft de volgende structuur:

| Naam | Type | Beschrijving |
| --- | --- | --- |
| reactie | DeliveryResponse | Komt overeen met het antwoord [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) |
| target_cookie | dict | [!DNL Target] cookie |
| target_location_hint_cookie | dict | [!DNL Target] locatiehintcookie |
| analytics_details | lijst [ AnalyticsResponse ] | [!DNL Analytics] payload, in het geval van [!DNL Analytics] gebruik op de client |
| traceren | lijst [ dict ] | Samengevoegde spoorgegevens voor alle verzoekdozen/meningen |
| response_tokens | lijst [ dict ] | Een lijst met [&#x200B; &#x200B; Responstkens &#x200B;](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=nl-NL) |
| meta | dict | Aanvullende beslissingsmetagegevens voor gebruik met apparaatbesluitvorming |

## Voorbeeld

Eerst bouwen we de [!UICONTROL Target Delivery API] -aanvraag voor het vooraf instellen van inhoud voor de vakken `home` en `product1` .

### Python

```python {line-numbers="true"}
mboxes = [MboxRequest(name="home"),
          MboxRequest(name="product1")]
prefetch = PrefetchRequest(mboxes=mboxes)
delivery_request = DeliveryRequest(prefetch=prefetch)

# Next, we fetch the offers via Target Python SDK getOffers() API
response = target_client.get_offers({ "request": delivery_request })
```

Een succesvol antwoord bevat een reactieobject [!UICONTROL Target Delivery API] dat vooraf gecodeerde inhoud bevat voor de gevraagde vakjes. Een voorbeeldobject `target_response["response"]` (opgemaakt als een dict) kan er als volgt uitzien:

### Python

```python {line-numbers="true"}
{
  "status": 200,
  "requestId": "e8ac2dbf5f7d4a9f9280f6071f24a01e",
  "id": {
    "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "client": "adobetargetmobile",
  "edgeHost": "mboxedge21.tt.omtrdc.net",
  "prefetch": {
    "mboxes": [
      {
        "index": 0,
        "name": "home",
        "options": [
          {
            "type": "html",
            "content": "HOME OFFER",
            "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
            "responseTokens": {
              "profile.memberlevel": "0",
              "geo.city": "dublin",
              "activity.id": "302740",
              "experience.name": "Experience B",
              "geo.country": "ireland"
            }
          }
        ],
        "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
      },
      {
        "index": 1,
        "name": "product1",
        "options": [
          {
            "type": "html",
            "content": "TEST OFFER 1",
            "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
            "responseTokens": {
              "profile.memberlevel": "0",
              "geo.city": "dublin",
              "activity.id": "302740",
              "experience.name": "Experience B",
              "geo.country": "ireland"
            }
          }
        ],
        "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
      }
    ]
  }
}
```

Noteer de velden mbox `name` en `state` en `eventToken` in elk van de opties voor de doelinhoud. Deze gegevens moeten in het `send_notifications()` -verzoek worden opgegeven zodra elke inhoudsoptie wordt weergegeven. Stel dat de `product1` mbox is weergegeven op een niet-browserapparaat. De aanmeldingsaanvraag zal als volgt worden weergegeven:

### Python

```python {line-numbers="true"}
notification_mbox = NotificationMbox(name="product1",
                                     state="J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U")
notification = Notification(
    id="1",
    type=MetricType.DISPLAY,
    timestamp=1621530726000,  # Epoch time in milliseconds
    mbox=notification_mbox,
    tokens=["t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="]
)
notification_request = DeliveryRequest(notifications=[notification])
```

Merk op dat zowel de mbox-status als het gebeurtenistoken zijn opgenomen die overeenkomen met de aanbieding van [!DNL Target] in het Prefetch-antwoord. Nadat we de aanvraag voor meldingen hebben gemaakt, kunnen we deze via de API-methode [!DNL Target] naar `send_notifications()` verzenden:

### Python

```python {line-numbers="true"}
response = target_client.send_notifications({ "request": notification_request })
```
