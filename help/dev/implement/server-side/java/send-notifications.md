---
title: Weergave- of klikberichten verzenden naar [!DNL Adobe Target] gebruiken van de SDK van Java
description: Leer hoe u sendNotifications() kunt gebruiken om weergave te verzenden of op meldingen te klikken naar [!DNL Adobe Target] voor meting en rapportage.
feature: APIs/SDKs
exl-id: 9231b480-f50f-40d1-ab06-0b9f2a2d79e3
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# Meldingen verzenden (Java)

## Beschrijving

`sendNotifications()` wordt gebruikt voor het verzenden van weergave- of klikberichten naar [!DNL Adobe Target] voor meting en rapportage.

>[!NOTE]
>
>Wanneer een `execute` object met vereiste parameters zich in het verzoek zelf bevindt, wordt de indruk automatisch vergroot voor in aanmerking komende activiteiten.

De methodes van SDK die een indruk automatisch zullen verhogen zijn:

* `getOffers()`
* `getAttributes()`

Wanneer een `prefetch` object binnen het verzoek wordt doorgegeven, wordt de indruk niet automatisch verhoogd voor de activiteiten met selectievakjes binnen het `prefetch` object. `sendNotifications()` moet worden gebruikt voor vooraf opgemaakte ervaringen voor het verhogen van indrukken en omzettingen.

## Methode

### maken

```javascript {line-numbers="true"}
ResponseStatus TargetClient.sendNotifications(TargetDeliveryRequest request)
```

## Voorbeeld

Laten we eerst de [!DNL Target Delivery API] verzoek om inhoud vooraf in te stellen voor de `home` en `product1` box.

### Prefetch

```javascript {line-numbers="true"}
List<MboxRequest> mboxRequests = new ArrayList<>();
mboxRequests.add((MboxRequest) new MboxRequest().name("home").index(1));
mboxRequests.add((MboxRequest) new MboxRequest().name("product1").index(2));
PrefetchRequest prefetchMboxesRequest = new PrefetchRequest().setMboxes(mboxRequests)

// Next, we fetch the offers via Target Java SDK getOffers() API
TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
```

Een succesvol antwoord bevat een [!UICONTROL Target Delivery API] reactieobject, dat vooraf ingestelde inhoud voor de gevraagde vakken bevat. Een monster `targetResponse.response` Het object kan er als volgt uitzien:

### Antwoord

```javascript {line-numbers="true"}
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

Noteer de mbox `name` en `state` en de `eventToken` in elk van de [!DNL Target] inhoudsopties. Deze moeten worden vermeld in het `sendNotifications()` aanvragen, zodra elke inhoudsoptie wordt weergegeven. Laten we aannemen `product1` mbox is weergegeven op een niet-browserapparaat. De aanmeldingsaanvraag ziet er als volgt uit:

### Verzoek

```javascript {line-numbers="true"}
TargetDeliveryRequest mboxNotificationRequest = TargetDeliveryRequest.builder().notifications(new ArrayList() {{
    add(new Notification()
            .id("1")
            .timestamp(System.currentTimeMillis())
            .type(MetricType.DISPLAY)
            .mbox(new NotificationMbox()
                    .name("product1")
                    .state("J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U")
            )
            .tokens(Arrays.asList(new String[]{"t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="}))
    );
}}).build();
```

Merk op dat wij zowel de mbox staat als de gebeurtenisteken hebben omvat die aan het overeenkomende [!DNL Target] voorstel geleverd in de prefetch reactie. Nadat we het verzoek om meldingen hebben samengesteld, kunnen we het verzenden naar [!DNL Target] via `sendNotifications()` API-methode:

### Antwoord

```javascript {line-numbers="true"}
ResponseStatus notificationResponse = targetJavaClient.sendNotifications(mboxNotificationRequest);
```
