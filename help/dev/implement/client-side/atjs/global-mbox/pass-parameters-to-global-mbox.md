---
keywords: algemene mbox-parameters, targetPageParams, queryreeks, array, json, dtm
description: Leer hoe u de [!UICONTROL targetPageParams] functie om extra het richten of contextinformatie in te gaan [!DNL Adobe Target] global mbox.
title: Hoe geef ik Parameters aan een Globale doos door?
feature: at.js
exl-id: 2a6be3e4-a618-4812-9e87-b01789705c40
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# Parameters doorgeven aan een globale box

JavaScript `targetPageParams` functie wordt gebruikt om parameters door te geven aan de algemene mbox in [!DNL Adobe Target]. Dit is nodig in elk scenario waarin aanvullende informatie over doelgerichtheid/context moet worden doorgegeven [!DNL Target].

In een Recommendations-activiteit gebruikt u bijvoorbeeld de parameters om het huidige product of de categorie te vertegenwoordigen die wordt weergegeven.

De code die de JavaScript-functie moet aanroepen, moet vóór het globale vakje op de pagina komen, ongeacht of het globale vakje als onderdeel van at.js is geactiveerd of handmatig in de paginacode is opgenomen.

>[!NOTE]
>
>Als u parameters wilt toevoegen aan alle vakken op de pagina en niet alleen aan de globale box, gebruikt u de optie [targetPageParamsAll()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md) functie.

U kunt parameters doorgeven aan `target-global-mbox` met de `targetPageParams()` op een van de volgende manieren te werken:

* Een array
* Een JSON-object
* Een door ampersand gescheiden lijst

Gebruik deze drie methoden om te controleren of de parameters correct worden doorgegeven. Mogelijk kunt u ook controleren of parameters zijn doorgegeven met de opdracht [Adobe Experience Cloud Debugger](https://experienceleague.adobe.com/docs/debugger/using/experience-cloud-debugger.html).

U moet de JavaScript-functie definiëren voordat u het globale vakje aan de pagina toevoegt. De naam moet `targetPageParams`.

## Tekenreeks query

```
p1=v1&p2=v2&p3=hello%20world
```

* Naam: `targetPageParams`
* Geretourneerde waarde: een &quot;&amp;&quot; gescheiden parameters, met URL-gecodeerde parameterwaarden.

  Voorbeeld:

  In dit voorbeeld heeft p3 de waarde `hello world`, die URL-gecodeerd is.

Overweeg de volgende voorbeeldpaginacode:

```html {line-numbers="true"}
<html> 
  <head> 
    <title>Title here..</title> 
    <script type="text/javascript"> 
        function targetPageParams() { 
          return "p1=v1&p2=v2&p3=hello%20world";
        } 
    </script> 
    <script src="mbox.js" type="text/javascript"></script> 
  </head> 
  <body>Body here... 
  </body> 
</html>
```

In dit voorbeeld worden de volgende gegevens naar de mbox-rand verzonden:

* p1=v1
* p2=v2
* p3=hello wereld

## Array

```javascript {line-numbers="true"}
<!--window.-->targetPageParams = function() { 
  return ["a=1", "b=2", "c=hello world"]; 
}; 
```

Waarden hoeven niet via URL te worden gecodeerd. Als een waarde bijvoorbeeld een spatie bevat, is het niet nodig de spatie te coderen.

In dit voorbeeld worden de volgende gegevens naar de mbox-rand verzonden:

* a=1
* b=2
* c=hello wereld

## JSON

JSON is een krachtige manier om parameters door te geven. [!DNL Target] gebruikt de JSON-objectsleutels om gecompliceerde structuren samen te voegen tot eenvoudige parameters.

```json {line-numbers="true"}
<!--window.-->targetPageParams = function() { 
  return { 
    "a": 1, 
    "b": 2, 
    "profile": { 
                  "memberStatus": Gold, 
                  "country": { 
                                "city": "San Francisco" 
                            } 
              } 
  }; 
}; 
```

Waarden hoeven niet via URL te worden gecodeerd. &quot;San Francisco&quot; vereist bijvoorbeeld niet dat de ruimte wordt gecodeerd. Een spatie volstaat.

In dit voorbeeld worden de volgende gegevens naar de mbox-rand verzonden:

* a=1
* b=2
* `profile.memberStatus`=Goud
* `profile.country.city`=San Francisco
