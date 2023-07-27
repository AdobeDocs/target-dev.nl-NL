---
keywords: targetPageParams, targetPageParams, pageParams, pageparams, pageParams, pageParameters, at.js, functions, function, targetPageParams0
description: Gebruik de [!UICONTROL targetPageParams()] functie voor de [!DNL Adobe Target] op.js JavaScript-bibliotheek om parameters van buiten de aanvraagcode toe te voegen aan het globale vak.
title: Hoe gebruik ik de [!UICONTROL targetPageParams()] Functie?
feature: at.js
exl-id: 274e4d1f-843a-443b-ad98-7139dc4a13f8
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# [!UICONTROL targetPageParams()]

Met deze methode kunt u parameters aan de globale mbox koppelen van buiten de aanvraagcode.

Deze functie is zeer nuttig om de zelfde reeks parameters op veelvoudige mbox vraag te omvatten. De functie moet door de klant worden gedefinieerd. Het zou een serie van parameters moeten terugkeren die slechts tot het globale mbox verzoek zullen worden overgegaan. Deze functie kan worden gedefinieerd voordat at.js wordt geladen of in **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit]** > **[!UICONTROL Library Header]**.

U kunt parameters aan target-global-mbox overgaan gebruikend `[!UICONTROL targetPageParams()]` op een van de volgende manieren te werken:

* Een door ampersand gescheiden lijst
* Een array
* Een JSON-object

## Voorbeelden

Door ampersand gescheiden lijst (waarden moeten URL-gecodeerd zijn):

```javascript {line-numbers="true"}
function targetPageParams() { 
    return "param1=value1&param2=value2&p3=hello%20world"; 
}
```

Array (waarden hoeven niet via URL te worden gecodeerd):

```javascript {line-numbers="true"}
targetPageParams = function() { 
     return ["a=1", "b=2", "c=hello world"]; 
};
```

JSON (waarden hoeven niet via URL te worden gecodeerd):

```javascript {line-numbers="true"}
targetPageParams = function() { 
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
