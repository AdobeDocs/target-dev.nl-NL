---
title: Implementatiepatroon voor aanbevelingen met behulp van at.js
description: Begrijp hoe te om het implementatiepatroon voor Aanbevelingen met at.js te gebruiken
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: d568cd1d-acc3-42e0-ae2c-5787e6f361f8
source-git-commit: 3b0bc0b67800ed4b1da6ba2bfa05c677147a78ba
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# [!DNL Recommendations] implementatiepatroon met behulp van het overzicht at.js

Dit implementatiepatroon helpt u uw [!DNL Adobe Target Recommendations] implementatie begrijpen en creëren wanneer het gebruiken van de {[ bibliotheek 1} at.js van JavaScript.](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)

Klik op de afbeelding om deze uit te breiden naar het volledige scherm.

![ Adobe Target architectuurdiagram ](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

De nummers in de afbeelding geven geen bewerkingsvolgorde aan:

1. Client-side SDK&#39;s voor [!DNL Adobe Target] en [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] oproep
1. Aankoopoproep [!UICONTROL Experience Cloud ID] (ECID)
1. Bulkprofielupdate-API en [!DNL Customer Attributes] (CA)-service
1. Profiel van gegevensinvoer van de gegevensbronnen van de klant naar het [!DNL Target] profielarchief
1. Profiel- en gedragsgegevens verzamelen en bepalen welke ervaring de bezoeker te zien krijgt
1. Ervaringen die op de pagina worden weergegeven
1. at.js geeft de ervaringen op de pagina weer

Elk patroon bestaat uit verschillende onderdelen, waarbij elk onderdeel overeenkomt met een essentiële implementatievereiste voor uw [!DNL Target] -implementatie.

Elk onderdeel wordt in een afzonderlijk artikel in deze handleiding uitgelegd:

* [SDKS initialiseren](/help/dev/patterns/recs-atjs/initialize-sdk.md)
* [Gegevensverzameling configureren](/help/dev/patterns/recs-atjs/data-collection.md)
* [Renderervaringen](/help/dev/patterns/recs-atjs/render-experiences.md)
* [Doel op hoogte stellen](/help/dev/patterns/recs-atjs/notify-target.md)
