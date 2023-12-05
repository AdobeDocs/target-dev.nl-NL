---
title: Adobe Target Delivery API Getting Started
description: Hoe gebruik ik de [!UICONTROL Adobe Target Delivery API]?
keywords: aflevering api
exl-id: 142ec3be-b017-4cdc-9079-b1cc173a710a
feature: APIs/SDKs
source-git-commit: e5a1c38d448cb7446b7b26cd0dc882976ba94dd3
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Aan de slag met de [!UICONTROL Adobe Target Delivery API]

A [!UICONTROL Target Delivery API] de vraag kijkt als dit:

```
curl -X POST \
  'https://`clientCode`.tt.omtrdc.net/rest/v1/delivery?client=`clientCode`&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
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
            "name" : "homepage",
            "index" : 1
          }
        ]
      }
    }'
```

De `clientCode` kan worden opgehaald uit de [!DNL Target] UI door te navigeren naar **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

Voordat u een [!UICONTROL Target Delivery API] de vraag, volgt deze stappen om ervoor te zorgen een antwoord de relevante ervaring bevat om eind - gebruikers te tonen:

1. Een [!DNL Target] activiteit (A/B, XT, AP of Recommendations) die het [Op formulier gebaseerde composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en) of de [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).
1. Gebruik de leverings-API om een antwoord te krijgen voor de vakken die worden gebruikt in de [!DNL Target] activiteit die in Stap 2 wordt gecreeerd.
1. Presenteer de ervaring aan de bezoeker.
