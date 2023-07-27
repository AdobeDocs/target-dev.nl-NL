---
keywords: mboxDefine, mboxdefine, mbox define, mboxUpdate, mbox update, mbox update, at.js, functions, function, mboxDefine0
description: Gebruik de [!UICONTROL mboxDefine()] en [!UICONTROL mboxUpdate()] functies voor de [!DNL Adobe Target] JavaScript-bibliotheek at.js om een box te definiëren of bij te werken. (om 1.js)
title: Hoe gebruik ik de [!UICONTROL mboxDefine()] en [!UICONTROL mboxUpdate()] Functies?
feature: at.js
exl-id: 0a7dbea2-1cbd-4a5b-ba68-4c76a88d65c4
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# [!UICONTROL mboxDefine()] en [!UICONTROL mboxUpdate()] - om.js 1.x

Een box definiëren en bijwerken in [!DNL Adobe Target].

>[!NOTE]
>
>Deze functies zijn beschikbaar voor at.js versies 1.*x* alleen. Deze functies zijn vervangen door de release van at.js 2.*x*. Deze functies retourneren standaardinhoud als deze wordt gebruikt met at.js 2.*x*.

`[!UICONTROL mboxDefine()]` en `[!UICONTROL mboxCreate()]` zijn gebonden aan HTML DIV-elementen waar het aanbod moet worden weergegeven. Deze HTML DIV-elementen moeten `mboxDefault` klasse. Als deze klasse niet wordt gekoppeld aan de HTML-elementen, ziet u een merkbare flikkering.

## mboxDefine

Maakt een interne toewijzing tussen een nodeId en een naam van een box, maar voert de aanvraag niet uit. Wordt gebruikt in combinatie met `[!UICONTROL mboxUpdate()]`. Gebouwd in at.js vooral om de overgang van mbox.js (nu afgekeurd) aan at.js te vergemakkelijken.

## mboxUpdate

Voert het verzoek uit en past het aanbod toe op het element dat door de `nodeId` in de `mboxDefine()`. Kan ook worden gebruikt om een box bij te werken die is gestart door `[!UICONTROL mboxCreate]`. Gebouwd in at.js vooral om de overgang van mbox.js (nu afgekeurd) aan at.js te vergemakkelijken. `mboxDefine()`/ `mboxUpdate()` kan worden vervangen door [adobe.target.getOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) en [adobe.target.applyOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) met de optie Selector.

## Voorbeeld

```javascript {line-numbers="true"}
<div id="someId" class="mboxDefault"></div> 
<script> 
 mboxDefine('someId','mboxName','param1=value1','param2=value2'); 
 mboxUpdate('mboxName','param3=value3','param4=value4'); 
</script>
```
