---
title: Overzicht van implementatiepatronen
description: Begrijpen hoe implementatiepatronen worden gebruikt
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 7a79eb1d263cf42529a5a1b1ca1f9de4db218a49
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Overzicht van implementatiepatronen

[!DNL Adobe Target] implementatiepatronen helpen u de volgende architectuur voor uw [!DNL Target] uitvoering.

Klik op de afbeelding om deze uit te breiden naar het volledige scherm.

![Adobe Target-architectuurdiagram](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

De nummers in de afbeelding geven geen bewerkingsvolgorde aan:

1. Client-side SDK&#39;s voor [!DNL Adobe Target] en [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] call
1. Aankoopoproep voor ECID
1. Bulkprofielupdate-API en [!DNL Customer Attributes] (CA)
1. Gegevensinvoer van gegevens van de klant naar [!DNL Target] profielarchief
1. Profiel-/gedragsgegevens verzamelen en bepalen welke ervaring de eindgebruiker te zien krijgt
1. Ervaringen die op de pagina worden weergegeven
1. at.js geeft de ervaringen op de pagina weer

Elk patroon bestaat uit verschillende onderdelen. Elk onderdeel voldoet aan een essentiële implementatievereiste voor uw [!DNL Target] uitvoering.

Elk onderdeel wordt uitgelegd op een aparte pagina in deze handleiding. Bijvoorbeeld de [[!DNL Recommendations] implementatiepatroon met behulp van at.js](/help/dev/patterns/recs-atjs/recs-implementation-pattern-atjs.md) bevat de volgende pagina&#39;s:

* SDK initialiseren
* Gegevensverzameling configureren
* Ervaringen renderen
* Waarschuwen [!DNL Target]

