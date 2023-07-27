---
title: Adobe Target Delivery API Identifier Visitors
description: Hoe kan ik een gebruiker identificeren binnen [!DNL Adobe Target]?
keywords: aflevering api
exl-id: 5b8c28aa-caad-44a9-880a-3c5f844e47b2
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# Bezoekers identificeren

Er zijn meerdere manieren waarop een bezoeker binnen [!DNL Adobe Target].

Doel gebruikt drie id&#39;s:

| Veldnaam | Beschrijving |
| --- | --- |
| `tntId` | De `tntId` is de primaire id in [!DNL Target] voor een gebruiker. U kunt deze id of [!DNL Target] automatisch genereren als de aanvraag geen verzoek bevat. |
| `thirdPartyId` | De `thirdPartyId` is het herkenningsteken van uw bedrijf voor de gebruiker die u met elke vraag kunt verzenden. Wanneer een gebruiker zich bij de plaats van een bedrijf aanmeldt, leidt het bedrijf typisch tot een identiteitskaart die aan de rekening van de bezoeker, de loyaliteitskaart, het lidmaatschapsaantal, of andere toepasselijke herkenningstekens voor dat bedrijf gebonden is. |
| `marketingCloudVisitorId` | De `marketingCloudVisitorId` wordt gebruikt om gegevens tussen verschillende Adobe oplossingen samen te voegen en te delen. De `marketingCloudVisitorId` is vereist voor integratie met Adobe Analytics en Adobe Audience Manager. |
| `customerIds` | Samen met de Experience Cloud-bezoeker-id [klant-id&#39;s](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) en kan een voor authentiek verklaarde status voor elke bezoeker worden gebruikt. |

## [!DNL Target] ID

De [!DNL Target] ID of `tntId` kan worden beschouwd als een apparaat-id. Dit `tntId` wordt automatisch gegenereerd door [!DNL Target] als het niet in het verzoek wordt verstrekt. Daarna moeten de volgende verzoeken deze omvatten `tntId` om de juiste inhoud aan een apparaat te leveren dat door de gebruiker wordt gebruikt.

```http {line-numbers="true"}
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
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

De voorbeeldvraag hierboven toont aan dat a `tntId` hoeft niet te worden doorgegeven. In dit scenario: [!DNL Target]  genereert een `tntId` en in het antwoord, zoals hieronder getoond:

```URI {line-numbers="true"}
{
  "status": 200,
  "requestId": "5b586f83-890c-46ae-93a2-610b1caa43ef",
  "client": "demo",
  "id": {
      "tntId": "10abf6304b2714215b1fd39a870f01afc.28_20"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  ...
}
```

De gegenereerde `tntId` is `10abf6304b2714215b1fd39a870f01afc.28_20`. Let op dit `tntId` moet worden gebruikt bij het aanroepen van de [!UICONTROL Adobe Target Delivery API] voor dezelfde gebruiker tijdens sessies.

## Bezoeker-id Marketing Cloud

De `marketingCloudVisitorId` is een universele en permanente id die uw bezoekers identificeert voor alle oplossingen in de Experience Cloud. Wanneer uw organisatie de id-service implementeert, kunt u met deze id dezelfde sitebezoeker en de gegevens ervan identificeren in verschillende Experience Cloud-oplossingen, zoals Adobe Target, Adobe Analytics of Adobe Audience Manager. Houd er rekening mee dat de `marketingCloudVisitorId` is vereist bij het benutten en integreren met Analytics en Audience Manager.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "marketingCloudVisitorId": "10527837386392355901041112038610706884"
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

Bovenstaande voorbeeldvraag toont aan hoe een `marketingCloudVisitorId` die is opgehaald van de Experience Cloud ID-service, wordt doorgegeven aan Adobe Target. In dit scenario: [!DNL Target] genereert een `tntId` aangezien het niet binnen aan de originele vraag werd overgegaan die aan verstrekt zal worden in kaart gebracht `marketingCloudVisitorId` Zoals in de onderstaande reactie is vermeld.

## Id van derde partij

Als uw organisatie een id gebruikt om uw bezoeker te identificeren, kunt u `thirdPartyID` om inhoud te leveren. U moet echter de `thirdPartyID` voor elke [!UICONTROL Adobe Target Delivery API] bel je.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "thirdPartyId": "B234A029348"
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

De voorbeeldvraag hierboven toont a `thirdPartyId`, een permanente id die uw bedrijf gebruikt om een eindgebruiker te identificeren, ongeacht of deze via internet, mobiele of IoT-kanalen communiceert met uw bedrijf. Met andere woorden: `thirdPartyId` verwijst naar gebruikersprofielgegevens die via kanalen kunnen worden gebruikt. In dit scenario: [!DNL Target] genereert een `tntId`, aangezien het niet binnen aan de originele vraag werd overgegaan, die aan verstrekt zal worden in kaart gebracht `thirdPartyId` Zoals in de onderstaande reactie is vermeld.

```
{
    "status": 200,
    "requestId": "55de9886-bd14-4dee-819c-7d1633b79b90",
    "client": "demo",
    "id": {
        "tntId": "10abf6304b2714215b1fd39a870f01afc.28_20",
        "thirdPartyId": "B234A029348"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    ...
}
```

## Klant-id

[Klant-id&#39;s](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) kan worden toegevoegd en gekoppeld aan een Experience Cloud-bezoeker-id. Wanneer u `customerIds` de `marketingCloudVisitorId` moeten ook worden verstrekt. Bovendien kan een authentificatiestatus samen met elk worden verstrekt `customerId` voor elke bezoeker. Met de volgende verificatiestatus kan rekening worden gehouden:

| Status van verificatie | Gebruikersstatus |
| --- | --- |
| `unknown` | Onbekend of nooit geverifieerd. Deze status kan worden gebruikt voor scenario&#39;s zoals een bezoeker die op uw plaats door op een vertoningsreclame is geland te klikken. |
| `authenticated` | De gebruiker is momenteel geverifieerd met een actieve sessie op uw website of app. |
| `logged_out` | De gebruiker werd voor authentiek verklaard maar actief het programma geopend. De gebruiker bedoelde en bedoeld om van de voor authentiek verklaarde staat los te maken. De gebruiker wil niet meer worden beschouwd als geverifieerd. |

Houd er rekening mee dat alleen wanneer de id van de klant zich bevindt `authenticated` status Doel verwijst naar de gegevens van het gebruikersprofiel die zijn opgeslagen en gekoppeld aan de id van de klant. Als de klant-id zich bevindt in `unknown` of `logged_out` staat, zal de klant identiteitskaart worden genegeerd, en om het even welke gegevens van het gebruikersprofiel die met het kunnen worden geassocieerd zullen niet voor publiek het richten worden gebruikt.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e044f14e1faeeba02d6ab23439914e' \
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
        "marketingCloudVisitorId" : "2304820394812039",
        "customerIds": [{
          "id": "134325423",
          "integrationCode" : "crm_data",
          "authenticatedState" : "authenticated"
        }]
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
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

De voorbeeldvraag hierboven toont aan hoe te om een te verzenden `customerId` met een `authenticatedState`. Wanneer u een `customerId`de `integrationCode`, `id`, en `authenticatedState` en de `marketingCloudVisitorId` zijn vereist. De `integrationCode` is de alias van de [klantkenmerkbestand](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html) via CRS.

## Samengevoegd profiel

U kunt `tntId`, `thirdPartyID`, en `marketingCloudVisitorId` in hetzelfde verzoek. In dit scenario houdt Adobe Target de toewijzing van al deze id&#39;s bij en koppelt het deze aan een bezoeker. Meer informatie over profielen [samengevoegd en in real time gesynchroniseerd](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) de verschillende id&#39;s gebruiken.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e044f14e1faeeba02d6ab23439914e' \
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
        "marketingCloudVisitorId" : "2304820394812039",
        "tntId": "d359234570e044f14e1faeeba02d6ab23439914e.28_78",
        "thirdPartyId":"23423432"
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

De voorbeeldvraag hierboven toont aan hoe u kunt combineren `tntId`, `thirdPartyID`, en `marketingCloudVisitorId` in hetzelfde verzoek. Alle drie id&#39;s worden ook geretourneerd in de reactie.
