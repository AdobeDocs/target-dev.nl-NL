---
keywords: adobe.target.applyOffer, applyOffer, apply-aanbieding, apply-aanbieding, at.js, functies, functie, $8
description: Gebruik de [!UICONTROL adobe.target.applyOffer()] functie voor de [!DNL Adobe Target] JavaScript-bibliotheek at.js om de inhoud van het antwoord toe te passen.
title: Hoe gebruik ik de [!UICONTROL adobe.target.applyOffer()] Functie?
feature: at.js
exl-id: 957bbe92-8012-4bd5-95d6-1ae38b72bb16
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# [!UICONTROL adobe.target.applyOffer(options)]

Deze functie is bedoeld om de inhoud van de reactie toe te passen met [!DNL Adobe Target].

>[!NOTE]
>
>`applyOffer` vereist `mbox` parameter. Als er geen naam van het selectievakje is opgegeven, treedt er een fout op.

De parameter options is verplicht en heeft de volgende structuur:

| Sleutel | Type | Vereist | Beschrijving |
|--- |--- |--- |--- |
| mbox | String | Ja | Naam van vak<br />Met at.js 1.3.0 (en later) dwingt het Doel af dat de mbox sleutel wordt gebruikt. Deze sleutel is in het verleden vereist, maar Doel dwingt nu zijn gebruik af om ervoor te zorgen dat Doel juiste bevestiging heeft en klanten correct de functie gebruiken. |
| kiezer | String of DOM Element | Nee | HTML-element of CSS-kiezer die wordt gebruikt om het HTML-element aan te duiden waar Target de aanbiedingsinhoud moet plaatsen. Als de selecteur niet wordt verstrekt, veronderstelt het Doel dat het element van de HTML HTML HEAD zou moeten gebruiken. |
| Voorstel | Array | Ja | Een array die op het element moet worden toegepast. |

## Voorbeeld

In het volgende voorbeeld wordt getoond hoe u `[!UICONTROL getOffer]` en `[!UICONTROL applyOffer]` samen:

```javascript {line-numbers="true"}
adobe.target.getOffer({   
  "mbox": "mbox",   
  "success": function(offers) {           
        adobe.target.applyOffer( {  
           "mbox": "mbox", 
           "offer": offers  
        } ); 
  },   
  "error": function(status, error) {           
      if (console && console.log) { 
        console.log(status); 
        console.log(error); 
      } 
  }, 
 "timeout": 5000 
}); 
```
