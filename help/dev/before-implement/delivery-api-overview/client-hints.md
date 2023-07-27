---
title: Adobe Target Delivery API Client Hints
description: Hoe gebruik ik de Tips van de Cliënt in [!DNL Adobe Target] Leverings-API?
exl-id: 317b9d7d-5b98-464e-9113-08b899ee1455
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# Clienttips en de [!UICONTROL Adobe Target Delivery API]

Clienttips moeten worden verzonden naar [!DNL Adobe Target] op de aanvraag voor aanbiedingen.

Over het algemeen wordt aangeraden alle beschikbare clienttips naar [!DNL Target]. Zie voor meer informatie [Gebruiker-agent en de wenken van de Cliënt](/help/dev/implement/client-side/atjs/user-agent-and-client-hints.md) in de [Implementatie op de client](../../implement/client-side/overview.md) sectie.

## Directe aanroepen van API voor levering

### Vanuit de browser

In dit geval verzendt de browser Client Hints met lage entropie naar [!DNL Target] automatisch via aanvraagheaders. Maar er zijn een paar browser-vlakke beperkingen met deze implementatie. Ten eerste - er worden geen kopteksten voor clienttips vanuit de browser verzonden, tenzij de aanvraag via https wordt gedaan. Tweede functie - Tips voor client worden niet verzonden op het eerste verzoek aan [!DNL Target] op de pagina. Clienttips worden alleen op het tweede verzoek en alle volgende aanvragen verzonden. Dit betekent dat publiekssegmentatie en personalisatie niet door kunnen worden uitgevoerd [!DNL Target] op de eerste pagina gaat u naar . Om rond beide beperkingen te krijgen, adviseren wij sterk gebruikend de Hints API van de Cliënt van de Agent van de Gebruiker in browser om de Hints van de Cliënt direct te verzamelen, en hen te verzenden op de verzoeklading.

### Van een server

In dit geval moet de Tips voor de client handmatig van de browser naar [!DNL Target] op de aanvraag voor de leverings-API.

```
curl -X POST 'http://mboxedge28.tt.omtrdc.net/rest/v1/delivery?client=myClientCode&sessionId=abcdefghijkl00014' -d '{
  "context": {
    "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Safari/537.36",
    "clientHints": {
      "Sec-CH-UA-Model": "iPhone",
      "Sec-CH-UA-Mobile": true,
      "Sec-CH-UA-Platform": "iOS",
      "Sec-CH-UA": "[ { \"brand\": \"Chromium\", \"version\": \"91\" }, { \"brand\": \" Not;A Brand\", \"version\": \"99\" } ]",
      "Sec-CH-UA-Full-Version-List": "[ { \"brand\": \"Chromium\", \"version\": \"91.1.1.1\" }, { \"brand\": \" Not;A Brand\", \"version\": \"99.1.1.1\" } ]",
      "Sec-CH-UA-Platform-Version": "10.0.0",
      "Sec-CH-UA-Arch": "x86",
      "Sec-CH-UA-Bitness": "64"
    }
  },
  "execute": {
    "mboxes": [{
      "name": "home",
      "index": 1
    }]
  }
}'
```

## Opmaak

De kopballen Sec-CH-UA en Sec-CH-UA-Full-Version-List van de Hints van de cliënt hebben een verschillend formaat dan de resultaten van browser API van de Tips van de Cliënt (navigator.userAgentData.brands/navigator.userAgentData.getHighEntropyValues). Beide indelingen worden geaccepteerd door de bezorgings-API. De leverings-API zal de waarden normaliseren in de indeling die wordt gebruikt in de aanvraagheaders. Dit is belangrijk om in gedachten te houden wanneer u in profielscripts toegang krijgt tot de clienttips.
