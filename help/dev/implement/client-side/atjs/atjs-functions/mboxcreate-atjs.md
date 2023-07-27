---
keywords: mboxCreate, mboxcreate, mbox create, at.js, functions, function
description: Gebruik de [!UICONTROL mboxCreate()] functie voor de [!DNL Adobe Target] in.js JavaScript-bibliotheek om aanbiedingen toe te passen op de dichtstbijzijnde DIV met de naam van de klasse mboxDefault. (om 1.js)
title: Hoe gebruik ik de [!UICONTROL mboxCreate()] Functie?
feature: at.js
exl-id: 86eba1fc-4e1d-4793-94e7-898bf81f8945
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# [!UICONTROL mboxCreate(mbox,params)] - om.js 1.x

Voert een verzoek uit en past de aanbieding op dichtstbijzijnde div met mboxDefault klassennaam toe.

>[!NOTE]
>
>Deze functie is beschikbaar voor at.js versies 1.*x* alleen. Deze functie is vervangen door de release van at.js 2.x. Deze functie retourneert standaardinhoud als deze wordt gebruikt met at.js 2.x.

Deze functie is vooral ingebouwd in at.js om de overgang van mbox.js (nu afgekeurd) naar at.js te vergemakkelijken. Een nieuwer alternatief voor `[!UICONTROL mboxCreate()]` is `[!UICONTROL adobe.target.getOffer()]`/ `[!UICONTROL adobe.target.applyOffer()]` of de Angular.

## Voorbeeld

```javascript {line-numbers="true"}
<div class="mboxDefault"> 
  default content to replace by offer 
</div> 
<script> 
  mboxCreate('mboxName','param1=value1','param2=value2'); 
</script>
```

## Notities

`mboxCreate()` gebruikt nu het &quot;json&quot;eindpunt in plaats van het &quot;standaard&quot;eindpunt en brand asynchroon. Daarom:

* [Foutopsporing](/help/dev/implement/client-side/target-debugging-atjs/target-debugging-atjs.md) is een beetje anders.
* Vermijd aanbiedingscode die synchrone, blokkerende vraag vereist.

  Bijvoorbeeld, aanbiedingen die variabelen plaatsen JavaScript die door plaatscode of andere dozen worden gebruikt die later op de pagina komen.

* Zorg ervoor dat u een `<div class="mboxDefault"></div>`voordat wordt aangeroepen `[!UICONTROL mboxCreate()]`, omdat om.js geen voor u zal toevoegen.

* Leeg, bovenaan pagina `[!UICONTROL mboxCreate()]` functies worden niet aanbevolen als een globale mbox.

  De automatisch gemaakte globale mbox in at.js is een betere optie omdat deze wordt geactiveerd van de `<head>` en kan inhoud eerder retourneren.
