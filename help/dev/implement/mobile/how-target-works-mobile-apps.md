---
description: Leer hoe u de [!DNL Adobe Mobile SDK] om de beste ervaringen te laten zien aan uw mobiele App-bezoekers.
title: Hoe werkt [!DNL Target] Werken in mobiele apps?
feature: Implement Mobile
exl-id: 33001f01-fde6-48cb-ac02-d1a632b2150d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Hoe [!DNL Target] werkt in mobiele apps

De [!DNL Adobe Mobile SDK] neemt contact op met [!DNL Target] om de inhoud samen met andere gegevenspunten op te halen, zodat de gebruiker de juiste ervaring krijgt.

>[!IMPORTANT]
>
>Steun voor de [!DNL Adobe Mobile] versie 4.*x* SDK&#39;s zijn geëindigd op 31 augustus 2021 en worden niet langer aanbevolen voor [!DNL Adobe Target] mobiele gebruikers.
>
>De [Adobe Experience Platform SDK voor mobiele apps](https://developer.adobe.com/client-sdks/documentation/){target=_blank} is de aanbevolen oplossing voor stroom [!DNL Adobe Experience Cloud] oplossingen en services in uw mobiele apps.

## [!DNL Target] locaties en succeswaarden

A *doellocatie* wordt ook mbox genoemd. Een geïdentificeerde locatie in de app is geschikt voor testen of personalisatie (bijvoorbeeld het welkomstbericht op het thuisscherm). Deze locaties worden tijdens het maken van de test geïdentificeerd.

A *[succesmetrisch](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=nl-NL)* is een actie die door de gebruiker wordt uitgevoerd en die aangeeft of een bepaalde activiteit succesvol was (zoals aanmelden, kopen, een ticket boeken, enzovoort).

![alternatieve afbeelding](assets/mobile-target-location.png)

* **[!DNL Target]locatie:** De inhoud die onder de registratieknop wordt weergegeven.

  Deze gebruiker krijgt gratis verzending tot 18.00 uur aangeboden. Deze locatie kan op meerdere locaties opnieuw worden gebruikt [!DNL Target] activiteiten om A/B-tests en personalisatie uit te voeren.

* **Metrisch resultaat:** De actie die wordt uitgevoerd door de gebruiker waar de gebruiker op de registratieknop tikt.

**Begrijpen hoe [!DNL Target] werkt in de SDK**

![alternatieve afbeelding](assets/how-target-mobile-works.png)
