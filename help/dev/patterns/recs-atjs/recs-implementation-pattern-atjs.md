---
title: Recommendations-implementatiepatroon met behulp van at.js
description: Begrijp hoe u het implementatiepatroon voor Recommendations kunt gebruiken met at.js
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 752c52c0db5173f49fd828c297fa7afd7c53c6ce
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# [!DNL Recommendations] implementatiepatroon met het overzicht van at.js

Dit implementatiepatroon helpt u uw kennis te begrijpen en uw [!DNL Adobe Target Recommendations] implementatie bij het gebruik van de [at.js JavaScript-bibliotheek](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md).

Klik op de afbeelding om deze uit te breiden naar het volledige scherm.

![Adobe Target-architectuurdiagram](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

De nummers in de afbeelding geven geen bewerkingsvolgorde aan:

1. Client-side SDK&#39;s voor [!DNL Adobe Target] en [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] call
1. [!UICONTROL Experience Cloud ID] (ECID) overnameoproep
1. Bulkprofielupdate-API en [!DNL Customer Attributes] (CA)
1. Gegevensinvoer van gegevens van de klant naar [!DNL Target] profielarchief
1. Profiel- en gedragsgegevens verzamelen en bepalen welke ervaring de bezoeker te zien krijgt
1. Ervaringen die op de pagina worden weergegeven
1. at.js geeft de ervaringen op de pagina weer

Elk patroon bestaat uit verschillende onderdelen, waarbij elk onderdeel overeenkomt met een essentiële implementatievereiste voor uw [!DNL Target] uitvoering.

Elk onderdeel wordt in een afzonderlijk artikel in deze handleiding uitgelegd:

* [SDKS initialiseren](/help/dev/patterns/recs-atjs/initialize-sdk.md)
* [Gegevensverzameling configureren](/help/dev/patterns/recs-atjs/data-collection.md)
* [Renderervaringen](/help/dev/patterns/recs-atjs/render-experiences.md)
* [Doel op hoogte stellen](/help/dev/patterns/recs-atjs/notify-target.md)

