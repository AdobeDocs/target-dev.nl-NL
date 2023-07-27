---
title: Overzicht van implementatiepatronen
description: Begrijpen hoe implementatiepatronen worden gebruikt
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: c4b9dfed19e5e4a56bfeae26c4310b997a2d617e
workflow-type: tm+mt
source-wordcount: '145'
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

Elk onderdeel wordt uitgelegd op een aparte pagina in deze handleiding. Bijvoorbeeld de [!DNL Target] het implementatiepatroon bevat de volgende pagina&#39;s:

* SDK initialiseren
* Profiel uitbreiden
* Ervaringen renderen
* Waarschuwen [!DNL Target]

