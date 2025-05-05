---
title: Adobe Target Delivery API-meldingen
description: Hoe vul ik meldingen in met de [!UICONTROL Adobe Target Delivery API]?
keywords: aflevering api
exl-id: 711388fd-2c1f-4ca4-939f-c56dc4bdc04a
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Meldingen

Meldingen moeten worden geactiveerd wanneer een vooraf ingestelde box of weergave is bezocht of weergegeven aan de eindgebruiker.

Als meldingen moeten worden afgespeeld voor de rechterbox of weergave, moet u de bijbehorende `eventToken` voor elke box of weergave. Meldingen met de juiste `eventToken` voor de overeenkomstige vakjes of meningen moeten in brand worden gestoken om correct verslag te worden weerspiegeld.

## Meldingen voor vooraf ingestelde maboxen

Een of meer meldingen kunnen via één leveringsoproep worden verzonden. Bepaal of de metrische waarde die moet worden bijgehouden een van beide is `click` of `display` voor elke box zodat de `type` van de kennisgeving correct kan worden weergegeven. Geef ook een `id` voor elk bericht zodat men kan bepalen of een bericht correct door[!UICONTROL &#x200B; Adobe Target Delivery API]. De `timestamp` is ook van belang om door te sturen naar [!DNL Target] om aan te geven wanneer de `click` of `display` is opgetreden voor een bepaalde box voor rapportagedoeleinden.

```
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '{
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
      "notifications": [
      {
      "id" : "SummerOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
      },
    {
      "id" : "SummerShoesOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerShoesOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
      },
    {
      "id" : "SummerDressOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerDressOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
    } 
    ]
  }'
```

De voorbeeldvraag hierboven zal in een reactie resulteren die op `notifications` aanvraag is verwerkt.

```
{
  "status": 200,
  "requestId": "36014eed-4772-4c48-a9e2-e532762b6a85",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.28_20"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "notifications": [
      {
          "id": "SummerOfferNotification"
      },
      {
          "id": "SummerDressOfferNotification"
      },
      {
          "id": "SummerShoesOfferNotification"
      }
  ]
}
```

Als alle `notifications` verzonden naar [!DNL Target] correct worden verwerkt, worden ze weergegeven in de `notifications` in de reactie. Als echter `notifications` `id` ontbreekt, dat specifieke `notification` is niet doorgegaan. In dit scenario zou een retry-logica kunnen worden ingevoerd tot een succesvol `notification` reactie wordt opgehaald. Zorg ervoor dat voor de logica voor opnieuw proberen een time-out is opgegeven zodat de API-aanroep geen vertraging van de prestaties oplevert.

## Meldingen voor vooraf ingestelde weergaven

Een of meer meldingen kunnen via één leveringsoproep worden verzonden. Bepaal of de metrische waarde die moet worden bijgehouden een van beide is `click` of `display` voor elke box zodat het type van het bericht correct kan worden weerspiegeld. Geef ook een `id` voor elk bericht zodat men kan bepalen of een bericht correct door [!UICONTROL Adobe Target Delivery API]. Het is ook belangrijk dat u de tijdstempel doorstuurt naar [!DNL Target] om aan te geven wanneer de `click` of `display` voor een bepaalde weergave is opgetreden voor rapportagedoeleinden.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
  },
  "context": {
    "channel": "web",
    "browser": {
      "host": "target.enablementadobe.com"
    },
    "address": {
      "url": "https://target.enablementadobe.com/react/demo/#/"
    }
  },
  "notifications": [{
      "id": "228",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "checkout-express",
      }
    },
    {
      "id": "5",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "home",
      }
    },
    {
      "id": "6",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "products",
      }
    }
  ]
}'
```

De voorbeeldvraag hierboven zal in een reactie resulteren die op `notifications` aanvraag is verwerkt.

```
{
    "status": 200,
    "requestId": "85cc7394-c19a-4398-9b8b-bbee1e4c4579",
    "client": "demo",
    "id": {
        "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "notifications": [
        {
            "id": "5"
        },
        {
            "id": "6"
        },
        {
            "id": "228"
        }
    ]
}
```

Als alle `notifications` verzonden naar  [!DNL Target] correct worden verwerkt, worden ze weergegeven in de `notifications` in de reactie. Als echter `notifications` `id` ontbreekt, is die specifieke kennisgeving niet doorgegaan. In dit scenario, zou een retry logica in plaats kunnen worden gebracht tot een succesvolle berichtreactie wordt teruggewonnen. Zorg ervoor dat voor de logica voor opnieuw proberen een time-out is opgegeven zodat de API-aanroep geen vertraging van de prestaties oplevert.
