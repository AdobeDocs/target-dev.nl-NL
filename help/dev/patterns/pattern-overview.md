---
title: Overzicht van implementatiepatronen
description: Begrijpen hoe implementatiepatronen worden gebruikt
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: e15513f5c52240536ccf41f16ba7f4dc6dbf9a04
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Overzicht van implementatiepatronen

[!DNL Adobe Target] implementatiepatronen helpen u de volgende architectuur voor uw [!DNL Target] uitvoering.

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

Elk deel wordt verklaard in een afzonderlijk onderwerp in deze gids. Bijvoorbeeld de [[!DNL Recommendations] implementatiepatroon met behulp van at.js](/help/dev/patterns/recs-atjs/recs-implementation-pattern-atjs.md) bevat de volgende onderwerpen :

* SDK initialiseren
* Gegevensverzameling configureren
* Ervaringen renderen
* Waarschuwen [!DNL Target]

