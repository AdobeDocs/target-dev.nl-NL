---
title: Integratie met Experience Cloud
description: Integratie met Experience Cloud
keywords: aflevering api
source-git-commit: f16903556954d2b1854acd429f60fbf6fc2920de
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

<!-- The content on this page was originally pulled from the legacy Delivery API doc site, and was subsequently found to be an outdated version of information now found on [Implement > Server-side > Integration > A4T Reporting](../../implement/server-side/sdk-guides/integration-with-experience-cloud/a4t-reporting.md) and [Implement > Server-side > Integration > AAM Segments](../../implement/server-side/sdk-guides/integration-with-experience-cloud/aam-segments.md). Therefore sunsetting this page, but not deleting it from the repo immediately, pending a more thorough examination to avoid inadvertently deleting relevant content. -->


# Integratie met Experience Cloud

## Adobe Analytics for Target (A4T)

Wanneer een vraag van de Levering API van het Doel van de server in brand wordt gestoken, keert Adobe Target de ervaring voor die gebruiker terug en bovenop dat, keert Adobe Target of de nuttige lading van Adobe Analytics terug naar de bezoeker of door:sturen het automatisch aan Adobe Analytics. Om de informatie van de activiteit van het Doel naar Adobe Analytics op de server te verzenden, zijn er een paar voorwaarden die moeten worden voldaan aan:

1. De activiteit wordt in de gebruikersinterface van Adobe Target ingesteld met Adobe Analytics als bron van rapportage en de accounts zijn ingeschakeld voor A4T
1. De Adobe Marketing Cloud-bezoeker-id wordt gegenereerd door de API-gebruiker en is beschikbaar wanneer de API-aanroep voor doellevering wordt geactiveerd

### Adobe Target stuurt de Payload van Analytics automatisch door

Adobe Target kan de lading van de analysegegevens automatisch via de serverzijde naar Adobe Analytics doorsturen als de volgende id&#39;s worden opgegeven:

1. `supplementalDataId` - De id die wordt gebruikt om te verbinden tussen Adobe Analytics en Adobe Target
1. `trackingServer` - De Adobe Analaytics Server zodat Adobe Target en Adobe Analytics de gegevens op de juiste wijze kunnen samenvoegen, hetzelfde `supplementalDataId` moeten zowel aan Adobe Target als aan Adobe Analytics worden doorgegeven.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
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
      "id": {
        "marketingCloudVisitorId": "2304820394812039"
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "analytics": {
          "supplementalDataId" : "23423498732598234",
          "trackingServer": "ags041.sc.omtrdc.net",
          "logging": "server_side"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          }
        ]
      }
    }'
```

### Analytics Payload van Adobe Target ophalen

Consumenten van de Adobe Target Delivery API kunnen de Adobe Analytics-lading voor een corresponderende doos ophalen zodat de consument de lading via de [API voor gegevensinvoer](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md). Wanneer een Adobe Target-aanroep op de server wordt geactiveerd, geeft u door `client_side` aan de `logging` in de aanvraag. Dit zal beurtelings een lading terugkeren als mbox in een activiteit aanwezig is die Analytics als rapporteringsbron gebruikt.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
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
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "analytics": {
          "logging": "client_side"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
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

Wanneer u `logging` = `client_side`, ontvangt u de lading in de `mbox` veld zoals hieronder weergegeven.

```
{
    "status": 200,
    "requestId": "4b8855a5-8354-4ac4-8ae7-c551f7c0bb8a",
    "client": "demo",
    "id": {
        "tntId": "d359234570e04f14e1faeeba02d6ab9914e.28_7"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "execute": {
        "mboxes": [
            {
                "index": 1,
                "name": "homepage",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                        "type": "html",

                    }
                ],
                "analytics": {
                    "payload": {
                        "pe": "tnt",
                        "tnta": "285408:0:0|2"
                    }
                }
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

Als de reactie van Doel iets in bevat `analytics` -> `payload` eigenschap, doorsturen naar Adobe Analytics. Analytics weet hoe deze lading moet worden verwerkt. Dit kan in een verzoek van de GET worden gedaan gebruikend het volgende formaat:

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/0/CODEVERSION?pe=tnt&tnta={payload}&mid={mid}&vid={vid}&aid={aid}
```

### Parameters en variabelen voor queryreeks

| Veldnaam | Vereist | Beschrijving |
| --- | --- | --- |
| `rsid` | Ja | De rapportsuite-id |
| `pe` | Ja | Pagina-gebeurtenis. Altijd instellen op `tnt` |
| `tnta` | Ja | Analyselading die door de server van het Doel in wordt geretourneerd `analytics` -> `payload` -> `tnta` |
| `mid` | Bezoeker-id Marketing Cloud |

### Vereiste koptekstwaarden

| Naam koptekst | Waarde koptekst |
| --- | --- |
| Host | Server voor gegevensverzameling voor analysemogelijkheden (bijv. adobeags421.sc.omtrdc.net) |

### Voorbeeld A4T Data Insertion HTTP Get Call

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0?pe=tnt&tnta=285408:0:0|2&mid=2304820394812039
```

## Adobe Audience Manager

Adobe Audience Manager (AAM)-segmenten kunnen ook worden benut via Adobe Target Delivery-API&#39;s. Voor het hefboomeffect AAM segmenten moeten de volgende velden worden verstrekt:

| Veldnaam | Vereist | Beschrijving |
| --- | --- | --- |
| `locationHint` | Ja | De Hint van de Plaats DCS wordt gebruikt om te bepalen welke AAM DCS Eindpunt om te slaan om het profiel terug te winnen. Moet >= 1 zijn. |
| `marketingCloudVisitorId` | Ja | Bezoeker-id Marketing Cloud |
| `blob` | Ja | AAM Blob wordt gebruikt om aanvullende gegevens naar AAM te verzenden. Mag niet leeg zijn en de grootte &lt;= 1024. |

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
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
      "id": {
        "marketingCloudVisitorId": "2304820394812039"
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "audienceManager": {
          "locationHint": 9,
          "blob": "32fdghkjh34kj5h43"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
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
