---
title: Weergave- of klikberichten verzenden naar [!DNL Adobe Target] het gebruiken van .NET SDK
description: Leer hoe u sendNotifications() kunt gebruiken om weergave te verzenden of op meldingen te klikken naar [!DNL Adobe Target] voor meting en rapportage.
feature: APIs/SDKs
exl-id: 724e787c-af53-4152-8b20-136f7b5452e1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Meldingen verzenden (.NET)

## Beschrijving

`SendNotifications()` wordt gebruikt voor het verzenden van weergave- of klikberichten naar [!DNL Adobe Target] voor meting en rapportage.

>[!NOTE]
>
>Wanneer een `Execute` object met vereiste parameters zich in het verzoek zelf bevindt, wordt de indruk automatisch vergroot voor in aanmerking komende activiteiten.

De methodes van SDK die een indruk automatisch zullen verhogen zijn:

* `GetOffers()`
* `GetAttributes()`

Wanneer een `Prefetch` object binnen het verzoek wordt doorgegeven, wordt de indruk niet automatisch verhoogd voor de activiteiten met selectievakjes binnen het `Prefetch` object. `SendNotifications()` moet worden gebruikt voor vooraf opgemaakte ervaringen voor het verhogen van indrukken en omzettingen.

## Methode

### Maken

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.SendNotifications(TargetDeliveryRequest request)
```

## Voorbeeld

Laten we eerst de [!UICONTROL Target Delivery API] verzoek om inhoud vooraf in te stellen voor de `home` en `product1` box.

### \.NET

```dotnet {line-numbers="true"}
var mboxRequests = new List<MboxRequest>
    {
        new (index: 1, name: "home"),
        new (index: 2, name: "product1"),
    };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .SetPrefetch(new PrefetchRequest(mboxes: mboxRequests))
    .Build();

// Next, we fetch the offers via Target .NET SDK GetOffers() API
var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
```

Een succesvol antwoord bevat een [!DNL Target Delivery API] reactieobject, dat vooraf ingestelde inhoud voor de gevraagde vakken bevat. Een monster `targetResponse.Response` Het object kan er als volgt uitzien:

### \.NET

```dotnet {line-numbers="true"}
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

Noteer de `mbox` naam en `state` en de `eventToken` in elk van de [!DNL Target] inhoudsopties. Deze moeten worden vermeld in het `SendNotifications()` aanvragen, zodra elke inhoudsoptie wordt weergegeven. Laten we aannemen `product1` mbox is weergegeven op een niet-browserapparaat. De aanmeldingsaanvraag zal als volgt worden weergegeven:

### \.NET

```dotnet {line-numbers="true"}
var mboxNotifications = new List<Notification>
{
    new (id: "1", type: MetricType.Display, timestamp: DateTimeOffset.UtcNow.ToUnixTimeMilliseconds(),
        mbox: new NotificationMbox("product1", "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"),
        tokens: new List<string> { "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" })
}; 

var mboxNotificationRequest = new TargetDeliveryRequest.Builder()
    .SetNotifications(mboxNotifications)
    .Build();
```

Er is zowel de mbox-status als de gebeurtenistoken opgenomen die overeenkomt met de [!DNL Target] voorstel geleverd in de prefetch reactie. Nadat we het verzoek om meldingen hebben samengesteld, kunnen we het verzenden naar [!DNL Target] via de `SendNotifications()` API-methode:

### \.NET

```dotnet {line-numbers="true"}
var notificationResponse = targetClient.SendNotifications(mboxNotificationRequest);
```
