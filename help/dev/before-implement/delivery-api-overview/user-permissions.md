---
title: Adobe Target Delivery API-gebruikersmachtigingen
description: Adobe Target Delivery API-gebruikersmachtigingen
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en#premium newtab=true" tooltip="Zie wat er in Target Premium is opgenomen."
keywords: aflevering api
exl-id: 332f90bd-4079-4653-aa38-b35837631c94
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Gebruikersmachtigingen (Premium)

[!DNL Adobe] kunnen klanten machtigingen voor hun gebruikers beheren wanneer ze Adobe Target gebruiken. Met het oog op een succesvolle [!UICONTROL Adobe Target Delivery API] aanroep, moet een token met de juiste machtigingen binnen de API-aanroep worden doorgegeven. Ga voor meer informatie over gebruikerstoegang en het ophalen van het token-bezoek [deze documentatie](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

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

Wanneer u de bijbehorende token hebt, geeft u deze door aan `property` -> `token` voor elke API-aanroep die wordt gemaakt. Als de `property` -> `token` niet binnen elke API-aanroep wordt doorgegeven, worden er geen `content` terug uit Adobe Target.

```
{
    "status": 200,
    "requestId": "07ce783d-58b9-461c-9f4c-6873aeb00c01",
    "client": "demo",
    "id": {
        "tntId": "d359234570e04f14e1faeeba02d6ab9914e.28_7"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "execute": {
        "mboxes": [
            {
                "index": 1,
                "name": "homepage"
            }
        ]
    }
}
```

Zoals u hierboven kunt zien, zonder het `property` -> `token`, krijgt u geen inhoud terug. Als u inhoud verwacht van uw API-aanroep, maar geen inhoud uit de reactie ophaalt, is dit waarschijnlijk omdat  `property` -> `token` wordt niet verstrekt, of het wordt overgegaan zonder de correcte toestemmingen.
