---
title: Adobe Target Delivery API Single of Batch Delivery
description: Hoe wordt ik gebruikt [!UICONTROL Adobe Target Delivery API] De enige of Vraag van de Levering van de Partij?
keywords: aflevering api
exl-id: 525cd1f2-616a-486c-8f49-8117615500bb
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Single of Batch-levering

De [!UICONTROL Adobe Target Delivery API] steunt één enkele of partijleveringsvraag. U kunt een serververzoek indienen voor inhoud voor een of meerdere vakken.

De prestatieskosten van het gewicht wanneer het beslissen om één enkele vraag tegenover een geveegde vraag te maken. Als u alle inhoud kent die voor een gebruiker moet worden getoond, is de beste praktijken inhoud voor alle dozen met één enkele vraag van de partijlevering terug te winnen, om het maken van veelvoudige enige leveringsvraag te vermijden.

## Single Delivery Call

U kunt een ervaring ophalen die u voor één box aan de gebruiker kunt weergeven via de [!UICONTROL Adobe Target Delivery API]. Merk op dat als u één enkele leveringsvraag maakt, u een andere servervraag zou moeten in werking stellen om extra inhoud voor een mbox voor een gebruiker terug te winnen. Dit kan in de loop der tijd zeer kostbaar worden, dus zorg ervoor dat u uw aanpak evalueert wanneer u de enige vraag van de leverings API gebruikt.

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
    "execute": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      }
    ]
  }
}'
```

In het enige bovenstaande voorbeeld van de leveringsvraag, wordt de ervaring teruggewonnen aan vertoning aan de gebruiker met `tntId`: `abcdefghijkl00023.1_1` voor een `mbox`:`SummerOffer` op het webkanaal. Deze enige leveringsvraag zal de volgende reactie produceren:

```
{
  "status": 200,
  "requestId": "25e0cc42-3d7b-456a-8b49-af60c1fb23d9",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.1_1"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "execute": {
      "mboxes": [
          {
              "index": 1,
              "name": "SummerOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                      "type": "html",
                  }
              ]
          }
      ]
    }
}
```

Let in het antwoord op het `content` bevat de HTML die de ervaring beschrijft die aan de gebruiker voor het Web moet worden getoond dat aan mbox SummerOffer beantwoordt.

### Pagina laden uitvoeren

Als er ervaringen zijn die moeten worden weergegeven wanneer een pagina in het webkanaal wordt geladen, zoals het testen van de lettertypen in de voettekst of de koptekst door AB&#39;s, kunt u `pageLoad` in de `execute` om alle wijzigingen op te halen die moeten worden toegepast.

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
  "execute": {
    "pageLoad": {}
  }
}'
```

De steekproefvraag hierboven wint om het even welke ervaringen terug om een gebruiker te tonen wanneer de pagina `https://target.enablementadobe.com/react/demo/#/` laden.

```
{
      "status": 200,
      "requestId": "355ebc47-edb6-481f-aeae-ae55d71afaca",
      "client": "demo",
      "id": {
          "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
      },
      "edgeHost": "mboxedge28.tt.omtrdc.net",
      "execute": {
          "pageLoad": {
              "options": [
                  {
                      "content": [
                          {
                              "type": "setHtml",
                              "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > NAV.nav:eq(0) > DIV.container:eq(0) > DIV.nav-right:eq(0) > A.nav-item:eq(0)",
                              "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > NAV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > A:nth-of-type(1)",
                              "content": "Modified Home"
                          }
                      ],
                      "type": "actions"
                  }
              ],
              "metrics": [
                  {
                      "type": "click",
                      "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > FORM.col-md-4:eq(0) > DIV.form-group:eq(0) > BUTTON.btn:eq(0)",
                      "eventToken": "QPaLjCeI9qKCBUylkRQKBg=="
                  }
              ]
          }
      }
  }
```

In de `content` kan de wijziging worden opgehaald die moet worden toegepast op het laden van een pagina. In het bovenstaande voorbeeld moet een koppeling in de koptekst een naam krijgen *Gewijzigd startpunt*.

## Vraag van de levering in batch

In plaats van het maken van veelvoudige leveringsvraag met één enkele mbox in elke vraag, die één leveringsvraag met een partij dozen maakt kan onnodige servervraag verminderen. Het aanroepen van een servervraag zou zoveel mogelijk moeten worden geminimaliseerd om hoogst presterend te zijn.

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
    "execute": {
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

In het batched leveringsvraagvoorbeeld hierboven, worden de ervaringen teruggewonnen aan vertoning voor de gebruiker met `tntId`: `abcdefghijkl00023.1_1` voor meerdere `mbox`:`SummerOffer`, `SummerShoesOffer`, en `SummerDressOffer`. Aangezien wij weten dat wij een ervaring voor veelvoudige dozen voor deze gebruiker moeten tonen, kunnen wij deze verzoeken in batch plaatsen en één servervraag in plaats van drie individuele leveringsvraag maken.

```
{
  "status": 200,
  "requestId": "fe15286f-effb-434f-85d8-c3db804075ce",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.28_120"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "execute": {
      "mboxes": [
          {
              "index": 1,
              "name": "SummerOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                      "type": "html",

                  }
              ]
          },
          {
              "index": 2,
              "name": "SummerShoesOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next shoe purchase</b></p>",
                      "type": "html",
                  }
              ]
          },
          {
              "index": 3,
              "name": "SummerDressOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next dress purchase</b></p>",
                      "type": "html",
                  }
              ]
          }
      ]
  }
}
```

In het bovenstaande antwoord kunt u dat zien binnen de `content` in het veld van elke mbox kan de HTML-weergave worden opgehaald van de ervaring die de gebruiker voor elke mbox te zien krijgt.
