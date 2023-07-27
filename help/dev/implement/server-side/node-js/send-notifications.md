---
title: Weergave- of klikberichten verzenden naar [!DNL Adobe Target] gebruiken van Node.js SDK
description: Leer hoe u sendNotifications() kunt gebruiken om weergave te verzenden of op meldingen te klikken naar [!DNL Adobe Target] voor meting en rapportage.
feature: APIs/SDKs
exl-id: 84bb6a28-423c-457f-8772-8e3f70e06a6c
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Meldingen verzenden (Node.js)

## Beschrijving

`[!UICONTROL sendNotifications()]` wordt gebruikt voor het verzenden van weergave- of klikberichten naar [!DNL Adobe Target] voor meting en rapportage.

>[!NOTE]
>
>Wanneer een `execute` object met vereiste parameters zich in het verzoek zelf bevindt, wordt de indruk automatisch vergroot voor in aanmerking komende activiteiten.

De methodes van SDK die een indruk automatisch zullen verhogen zijn:

* `getOffers()`
* `getAttributes()`

Wanneer een `prefetch` object binnen het verzoek wordt doorgegeven, wordt de indruk niet automatisch verhoogd voor de activiteiten met selectievakjes binnen het `prefetch` object. `sendNotifications()` moet worden gebruikt voor vooraf opgemaakte ervaringen voor het verhogen van indrukken en omzettingen.

## Methode

### maken

```js {line-numbers="true"}
TargetClient.sendNotifications(options: Object): Promise
```

### Parameters

`options` heeft de volgende structuur:

| Naam | Type | Vereist | Standaard |
| --- | --- | --- | --- |
| verzoek | Object | Ja | Geen |

## Voorbeeld

Eerst, bouwen wij het Doel Dleverings-API-aanvraag voor het vooraf instellen van inhoud voor de `home` en `product1` box.

### Node.js

```js {line-numbers="true"}
const prefetchMboxesRequest = {
  prefetch: {
    mboxes: [
      { name: "home" },
      { name: "product1" }
    ]
  }
};
// Next, we fetch the offers via Target Node.js SDK getOffers() API
const targetResponse = await targetClient.getOffers({ request: prefetchMboxesRequest });
```

Een succesvol antwoord bevat een [!UICONTROL Target Delivery API] reactieobject, dat vooraf ingestelde inhoud voor de gevraagde vakken bevat. Een monster `targetResponse.response` Het object kan er als volgt uitzien:

### Node.js

```js {line-numbers="true"}
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

Noteer de mbox `name` en `state` en de `eventToken` in elk van de [!DNL Target] inhoudsopties. Deze moeten worden vermeld in het `sendNotifications()` aanvragen, zodra elke inhoudsoptie wordt weergegeven. Laten we aannemen `product1` mbox is weergegeven op een niet-browserapparaat. De aanmeldingsaanvraag zal als volgt worden weergegeven:

### Node.js

```js {line-numbers="true"}
const mboxNotificationRequest = {
  notifications: [{
    id: "1",
    timestamp: Date.now(),
    type: "display",
    mbox: {
      name: "product1",
      state: "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
    },
    tokens: [ "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" ]
  }]
};
```

Merk op dat wij zowel de mbox staat als de gebeurtenisteken hebben omvat die aan het overeenkomende [!DNL Target] voorstel geleverd in de prefetch reactie. Nadat we het verzoek om meldingen hebben samengesteld, kunnen we het verzenden naar [!DNL Target] via de `sendNotifications()` API-methode:

### Node.js

```js {line-numbers="true"}
const notificationResponse = await targetClient.sendNotifications({ request: mboxNotificationRequest });
```
