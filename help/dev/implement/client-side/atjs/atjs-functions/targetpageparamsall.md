---
keywords: targetPageParamsAll, targetPageParamsAll, pageParamsAll, pageParams, pageParams, pageParameters, at.js, functions, function, targetPageParamsAll0
description: Gebruik de [!UICONTROL targetPageParamsAll()] functie voor de [!DNL Adobe Target] op.js JavaScript-bibliotheek om parameters toe te voegen aan alle vakken van buiten de aanvraagcode.
title: Hoe gebruik ik de [!UICONTROL targetPageParamsAll()] Functie?
feature: at.js
exl-id: 32045e60-6904-42a1-bf71-fd7e167a829f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# [!UICONTROL targetPageParamsAll()]

Met deze methode kunt u parameters koppelen aan alle vakken van buiten de aanvraagcode.

Dit is zeer nuttig om de zelfde reeks parameters op veelvoudige mbox vraag te omvatten. De functie moet door de klant worden gedefinieerd. Het zou een serie van parameters moeten terugkeren die aan alle mbox verzoeken op de pagina zullen worden overgegaan. Deze functie kan worden gedefinieerd voordat at.js wordt geladen of in **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit]** > **[!UICONTROL Code Settings]** > **[!UICONTROL Library Header]**.

U kunt parameters aan target-global-mbox overgaan gebruikend [!UICONTROL targetPageParamsAll()] op een van de volgende manieren te werken:

* Een door ampersand gescheiden lijst
* Een array
* Een JSON-object

## Voorbeelden

Door ampersand gescheiden lijst (waarden moeten URL-gecodeerd zijn):

```javascript {line-numbers="true"}
function targetPageParamsAll() { 
    return "param1=value1&param2=value2&p3=hello%20world"; 
}
```

Array (waarden hoeven niet via URL te worden gecodeerd):

```javascript {line-numbers="true"}
targetPageParamsAll = function() { 
     return ["a=1", "b=2", "c=hello world"]; 
};
```

JSON (waarden hoeven niet via URL te worden gecodeerd):

```javascript {line-numbers="true"}
targetPageParamsAll = function() { 
  return { 
    "a": 1, 
    "b": 2, 
    "profile": { 
        "age": 26, 
        "country": { 
          "city": "San Francisco" 
        } 
      } 
  }; 
};
```
