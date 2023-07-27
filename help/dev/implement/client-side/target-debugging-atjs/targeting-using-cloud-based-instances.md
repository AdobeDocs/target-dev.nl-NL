---
keywords: wolkeninstanties, openbare achtervoegsellijst, openbaar achtervoegsel, cookie, cookie van eerste partij, cookie van eerste partij, azurewebsites.net, cloudapp.net, amazonaws.com, cloudfront.net, herokuapp.com, firebaseapp.com, targetGlobalSettings, cookieDomain, cloud instances5, cloud instances6, cloud instances7, cloud instances8, cloud instances9, openbare achtervoegsellijst0, openbare achtervoegsel list1, openbaar achtervoegsel2, openbare achtervoegsel3, openbare achtervoegsellijst4 , openbare achtervoegsel list5
description: Problemen verkennen (met oplossingen) die klanten onder ogen zien wanneer ze cloudgebaseerde instanties gebruiken om te testen [!DNL Adobe Target] of voor conceptuele doeleinden.
title: Kan ik gebruiken [!DNL Target] met op cloud gebaseerde instanties?
feature: at.js
exl-id: 4b24fdc0-6c74-4b29-bbf9-7a761d4564a2
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Gebruik cloudgebaseerde instanties met [!DNL Target]

Informatie over problemen waarmee klanten worden geconfronteerd wanneer ze cloudgebaseerde instanties gebruiken om te testen [!DNL Adobe Target].

[!DNL Target] klanten gebruiken soms cloudgebaseerde instanties met [!DNL Target] voor tests of eenvoudige concepttest. Deze instanties kunnen de volgende domeinen omvatten:

`azurewebsites.net`, `cloudapp.net`, `amazonaws.com`, `cloudfront.net`, `herokuapp.com`, of `firebaseapp.com`

Deze en vele andere domeinen maken deel uit van de [Lijst met openbare achtervoegsels](https://publicsuffix.org/list/public_suffix_list.dat).

**Probleem:** Moderne browsers slaan geen cookies op als u deze domeinen gebruikt.

De JavaScript-bibliotheek at.js gebruikt cookies om gebruikers bij te houden om ervoor te zorgen dat [!DNL [!DNL Target]] biedt altijd een consistente ervaring. Als de [!DNL Target] JavaScript-bibliotheek kan geen cookies opslaan, doelaanvragen zijn uitgeschakeld.

**Oplossing:** Als beste praktijken, als u op wolk-gebaseerde instanties met domeinen inbegrepen op de Openbare Lijst van het Achtervoegsel van het Hoogtepunt wilt gebruiken, zorg ervoor dat u aanpast `cookieDomain` instellen. Zie voor meer informatie [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).
