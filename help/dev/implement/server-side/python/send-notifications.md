---
title: Weergave- of klikberichten verzenden naar [!DNL Adobe Target] met de Python SDK
description: Leer hoe u sendNotifications() kunt gebruiken om weergave te verzenden of op meldingen te klikken naar [!DNL Adobe Target] voor meting en rapportage.
feature: APIs/SDKs
exl-id: 03827b18-a546-4ec8-8762-391fcb3ac435
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# Meldingen verzenden (Python)

## Beschrijving

`send_notifications()` wordt gebruikt voor het verzenden van weergave- of klikberichten naar [!DNL Adobe Target] voor meting en rapportage.

>[!NOTE]
>
>Wanneer een `execute` object met vereiste parameters zich in het verzoek zelf bevindt, wordt de indruk automatisch vergroot voor in aanmerking komende activiteiten.

De methodes van SDK die een indruk automatisch zullen verhogen zijn:

* `get_offers()`
* `get_attributes()`

Wanneer een `prefetch` object binnen het verzoek wordt doorgegeven, wordt de indruk niet automatisch verhoogd voor de activiteiten met selectievakjes binnen het `prefetch` object. `Send_notifications()` moet worden gebruikt voor vooraf opgemaakte ervaringen voor het verhogen van indrukken en omzettingen.

## Methode

### send_notifications

```python {line-numbers="true"}
target_client.send_notifications(options)
```

## Parameters

`options` heeft de volgende structuur:

| Naam | Type | Vereist | Standaard | Beschrijving |
| --- | --- | --- | --- | --- |
| verzoek | DeliveryRequest | Ja | Geen | Hiermee wordt voldaan aan de [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) verzoek |
| target_cookie | str | nee | Geen | [!DNL Target] koekje |
| target_location_hint | str | nee | Geen | [!DNL Target] locatiehint |
| consumer_id | str | nee | Geen | Wanneer het stitching van veelvoudige vraag, zouden verschillende consument IDs moeten worden verstrekt |
| customer_ids | list[CustomerId] | nee | Geen | Een lijst met Customer Ids in de indeling VisitorId die compatibel is met de klant |
| session_id | str | nee | Geen | Wordt gebruikt voor het koppelen van meerdere aanvragen |
| callback | aanroepbaar | nee | Geen | Als het behandelen van verzoek asynchroon, callback wordt aangehaald wanneer de reactie klaar is |
| err_callback | aanroepbaar | nee | Geen | Als het behandelen van verzoek asynchroon, foutencallback wordt aangehaald wanneer de uitzondering wordt opgeheven |

## Retourneert

`Returns` a `TargetDeliveryResponse` indien synchroon (standaard), of een `AsyncResult` als opgeroepen met een callback. `TargetDeliveryResponse` heeft de volgende structuur:

| Naam | Type | Beschrijving |
| --- | --- | --- |
| reactie | DeliveryResponse | Hiermee wordt voldaan aan de [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) reactie |
| target_cookie | dict | [!DNL Target] koekje |
| target_location_hint_cookie | dict | [!DNL Target] locatiehintcookie |
| analytics_details | list[AnalyticsResponse] | [!DNL Analytics] lading, in geval van cliënt-kant [!DNL Analytics] gebruiken |
| traceren |  | list[dict] | Samengevoegde spoorgegevens voor alle verzoekdozen/meningen |
| response_tokens | list[dict] | Een lijst van [&#x200B; respontokens](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=nl-NL) |
| meta | dict | Aanvullende beslissingsmetagegevens voor gebruik met apparaatbesluitvorming |

## Voorbeeld

Laten we eerst de [!UICONTROL Target Delivery API] verzoek om inhoud vooraf in te stellen voor de `home` en `product1` box.

### Python

```python {line-numbers="true"}
mboxes = [MboxRequest(name="home"),
          MboxRequest(name="product1")]
prefetch = PrefetchRequest(mboxes=mboxes)
delivery_request = DeliveryRequest(prefetch=prefetch)

# Next, we fetch the offers via Target Python SDK getOffers() API
response = target_client.get_offers({ "request": delivery_request })
```

Een succesvol antwoord bevat een [!UICONTROL Target Delivery API] reactieobject, dat vooraf ingestelde inhoud voor de gevraagde vakken bevat. Een monster `target_response["response"]` Het object (opgemaakt als een dict) kan er als volgt uitzien:

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

Noteer de mbox `name` en `state` en de `eventToken` in elk van de opties voor doelinhoud. Deze moeten worden vermeld in het `send_notifications()` aanvragen, zodra elke inhoudsoptie wordt weergegeven. Laten we aannemen `product1` mbox is weergegeven op een niet-browserapparaat. De aanmeldingsaanvraag zal als volgt worden weergegeven:

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

Er is zowel de mbox-status als de gebeurtenistoken opgenomen die overeenkomt met de [!DNL Target] voorstel geleverd in de prefetch reactie. Nadat we het verzoek om meldingen hebben samengesteld, kunnen we het verzenden naar [!DNL Target] via de `send_notifications()` API-methode:

### Python

```python {line-numbers="true"}
response = target_client.send_notifications({ "request": notification_request })
```
