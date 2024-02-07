---
title: Adobe Target Delivery API Prefetch
description: Hoe gebruik ik Prefetch in de [!UICONTROL Adobe Target Delivery API]?
keywords: aflevering api
exl-id: eab88e3a-442c-440b-a83d-f4512fc73e75
feature: APIs/SDKs
source-git-commit: 803723d95d50cc39101d1646232446fbb0254385
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# Prefetch

Met Prefetching kunnen clients zoals mobiele apps en servers inhoud ophalen voor meerdere vakken of weergaven in één aanvraag, de inhoud lokaal in cache plaatsen en later op de hoogte brengen [!DNL Target] wanneer de gebruiker deze vakken of weergaven bezoekt.

Wanneer het gebruiken van prefetch, is het belangrijk om met de volgende termijnen vertrouwd te zijn:

| Veldnaam | Beschrijving |
| --- | --- |
| `prefetch` | Lijst met vakken en weergaven die moeten worden opgehaald maar niet moeten worden gemarkeerd als bezocht. De [!DNL Target] Edge retourneert een `eventToke`n voor elke box of weergave in de prefetch-array. |
| `notifications` | Lijst met vakken en weergaven die eerder waren voorafgegaan en die moeten worden gemarkeerd als bezocht. |
| `eventToken` | Een gehasht gecodeerd token dat wordt geretourneerd wanneer inhoud vooraf wordt geplaatst. Deze token moet worden teruggestuurd naar [!DNL Target] in de `notifications` array. |

## Prefetch Mboxes

Clients zoals mobiele apps en servers kunnen een voorvoegsel toevoegen aan meerdere vakken voor een bepaalde gebruiker binnen een sessie en deze in cache plaatsen om meerdere aanroepen naar [!UICONTROL Adobe Target Delivery API].

```
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=7abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '
{
  "id": {
    "tntId": "abcdefghijkl00023.1_1"
  },
  "context": {
    "channel": "web",
    "browser" : {
      "host" : "demo"
    },
    "address" : {
      "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
    },
    "screen" : {
      "width" : 1200,
      "height": 1400
    }
  },
    "prefetch": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      },
      {
        "name" : "SummerShoesOffer",
        "index" : 2
      },
      {
        "name" : "SummerDressOffer",
        "index" : 3
      }      
    ]
  }
}'
```

Binnen de `prefetch` veld, een of meer toevoegen `mboxes` U wilt een voorvertoning weergeven voor een gebruiker in een sessie. Zodra u voor hen vooraf instelt `mboxes` u ontvangt het volgende antwoord:

```
{
    "status": 200,
    "requestId": "5efee0d8-3779-4b12-a74e-e04848faf191",
    "client": "demo",
    "id": {
        "tntId": "abcdefghijkl00023.1_1"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "prefetch": {
        "mboxes": [
            {
                "index": 1,
                "name": "SummerOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            },
            {
                "index": 2,
                "name": "SummerShoesOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next shoe purchase</b></p>"
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            },
            {
                "index": 3,
                "name": "SummerDressOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next dress purchase</b></p>"
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            }
        ]
    }
}
```

In de reactie ziet u de `content` veld met de ervaring die de gebruiker voor een bepaalde `mbox`. Dit is erg handig wanneer u een cachegeheugen op de server plaatst, zodat een gebruiker tijdens een sessie communiceert met uw web of mobiele toepassing en een `mbox` op een bepaalde pagina van uw toepassing, kan de ervaring van het geheime voorgeheugen in plaats van het maken van een andere worden geleverd [!UICONTROL Adobe Target Delivery API] vraag. Wanneer de gebruiker echter een ervaring krijgt vanuit de `mbox`, `notification` wordt verzonden via een API-aanroep voor aflevering, zodat de afdruk kan worden geregistreerd. Dit komt omdat de reactie van `prefetch` de vraag wordt in het voorgeheugen ondergebracht, wat betekent dat de gebruiker de ervaringen op het tijdstip van `prefetch` de vraag gebeurt. Voor meer informatie over de `notification` proces, zie [Meldingen](notifications.md).

## Prefetch-vakken met clickTrack-meetgegevens bij gebruik [!UICONTROL Analytics for Target] (A4T)

[[!UICONTROL Adobe Analytics for Target]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html){target=_blank} (A4T) is een integratie met meerdere oplossingen waarmee u activiteiten kunt maken op basis van [!DNL Analytics] conversiemetriek en publiekssegmenten.

Het volgende codefragment is een reactie van een prefetch die een box bevat `clickTrack` cijfers voor meldingen [!DNL Analytics] dat op een voorstel is geklikt:

```
{
  "prefetch": {
    "mboxes": [
      {
        "index": 0,
        "name": "<mboxName>",
        "options": [
           ...
        ],
        "metrics": [
          {
            "type": "click",
            "eventToken": "<eventToken>",
             "analytics": {
               "payload": {
                 "pe": "tnt",
                 "tnta": "..."
               }
             }
          },
          }
        ],
        "analytics": {
          "payload": {
            "pe": "tnt",
            "tnta": "347565:1:0|2,347565:1:0|1"
          }
        }
      }
    ]
  }
}
```

>[!NOTE]
>
>De prefetch voor een box bevat de [!DNL Analytics] alleen voor gekwalificeerde activiteiten. Het vooraf bepalen van succeswaarden voor nog niet gekwalificeerde activiteiten leidt tot inconsistenties bij de rapportage.

## Vooraf ingestelde weergaven

Weergaven ondersteunen toepassingen voor één pagina (SPA) en mobiele toepassingen naadloos. Weergaven kunnen worden beschouwd als een logische groep visuele elementen die samen een SPA of mobiele ervaring vormen. Nu, door levering API, creeerde VEC AB &amp; XT activiteiten met wijzigingen op [Weergaven voor SPA](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md) kan nu vooraf worden ingesteld.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=a3e7368c62d944c0855d424cd7a03ab0' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
  },
  "context": {
    "channel": "web",
    "window": {
      "width": 1819,
      "height": 842
    },
    "browser": {
      "host": "target.enablementadobe.com"
    },
    "address": {
      "url": "https://target.enablementadobe.com/react/demo/#/"
    }
  },
  "prefetch": {
    "views": [{}]
  }
}'
```

De voorbeeldvraag hierboven zal alle Weergaven vooraf intypen die door SPA VEC voor AB en XT activiteiten worden gecreeerd om voor het Web te tonen `channel`. Bericht in de vraag dat wij alle Meningen van AB of XT activiteiten willen vooraf inrichten die een bezoeker met `tntId`:`84e8d0e211054f18af365d65f45e902b.28_131` die de `url`:`https://target.enablementadobe.com/react/demo/#/` kwalificeert voor.

```
{
    "status": 200,
    "requestId": "14ce028e-d2d2-4504-b3da-32740fa8dd61",
    "client": "demo",
    "id": {
        "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "prefetch": {
        "views": [
            {
                "id": 228,
                "name": "checkout-express",
                "key": "checkout-express",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setHtml",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > FORM.col-md-4:eq(0) > DIV:nth-of-type(1) > DIV.mb-3:eq(2)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(1) > FORM:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(3)",
                                "content": "<span style=\"color:#000080;\"><strong>*We charge an additional fee of $12.34 for faster delivery. If you choose express delivery get 15% off on your next order.</strong></span>"
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            },
            {
                "id": 5,
                "name": "home",
                "key": "home",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setHtml",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(1) > DIV.heading:eq(0) > H1.title:eq(0)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > H1:nth-of-type(1)",
                                "content": "<span style=\"color:#800000;\"><strong>Trending Items</strong></span>"
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            },
            {
                "id": 6,
                "name": "products",
                "key": "products",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setStyle",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > DIV.heading:eq(0) > BUTTON.btn:eq(0)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > BUTTON:nth-of-type(1)",
                                "content": {
                                    "background-color": "rgba(191,0,0,1)",
                                    "priority": "important"
                                }
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            }
        ]
    }
}
```

In de `content` velden van de reactie, metagegevens van notities zoals `type`, `selector`, `cssSelector`, en `content`, die worden gebruikt om de ervaring aan uw eind terug te geven - gebruiker wanneer een gebruiker uw pagina bezoekt. Let erop dat de `prefetched` inhoud kan in de cache worden opgeslagen en indien nodig aan de gebruiker worden gerenderd.
