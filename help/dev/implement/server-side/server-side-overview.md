---
keywords: server side, server side, api, sdk, node.js, nodejs, node js, recommendations api, api, apis, server side1
description: Meer informatie over de [!DNL Adobe Target] server-side levering-API's, SDK's en [!DNL Target Recommendations] API's.
title: Waar kan ik informatie over krijgen? [!DNL Target] Server-Side Delivery APIs en SDKs?
feature: Implement Server-side
exl-id: 3eb0a789-cf1a-4d02-acf7-3c895bcb662f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# Serverzijde: implementeren [!DNL Target]

Informatie over [!DNL Adobe Target] server-side levering-API&#39;s, SDK&#39;s en [!DNL Target Recommendations] API&#39;s.

Het volgende proces vindt plaats in een serverimplementatie van [!DNL Target]:

1. Een clientapparaat vraagt om een ervaring via de server.
1. Uw server verzendt die aanvraag naar [!DNL Target].
1. [!DNL Target] verzendt de reactie terug naar uw server.
1. Uw server bepaalt welke ervaring om aan het cliëntapparaat te leveren voor het terug te geven.

De ervaring hoeft niet in een browser te worden weergegeven. De ervaring kan in een e-mail of kiosk, via een stemmedewerker, of door één of andere andere niet-visuele ervaring of niet op browser-gebaseerd apparaat tonen. Omdat uw server tussen de client en [!DNL Target]Dit type implementatie is ook ideaal als u meer controle en beveiliging nodig hebt of complexe back-endprocessen hebt die u op uw server wilt uitvoeren.

>[!NOTE]
>
>Een nieuwe bezoeker kan alleen op de client worden geïnitialiseerd. Een nieuwe bezoeker *kan* worden geïnitialiseerd op de server. Dit is te wijten aan de ECID, die afhankelijk is van het demdex-cookie van derden en daarom moet worden geïnitialiseerd via Visitor API.js op een implementatie waarbij de browser betrokken is.

De volgende secties bevatten meer informatie over de verschillende API&#39;s en SDK&#39;s aan de serverzijde:

## Server Side Delivery-API&#39;s

Koppeling: [Server Side Delivery-API&#39;s](/help/dev/implement/delivery-api/overview.md)

`/rest/v1/delivery`

Via de [!DNL Target] Leverings-API, kunt u:

* Lever ervaringen over het web, met inbegrip van SPA, en mobiele kanalen evenals niet-browser gebaseerde IoT apparaten, zoals aangesloten TVs, kiosken, of in-store digitale schermen.
* Lever ervaringen van om het even welke server-zijplatform of toepassing die HTTP/s vraag kan maken.
* Lever consistente en gepersonaliseerde ervaringen aan een bezoeker ongeacht welk kanaal of welke apparaten de bezoeker gebruikte om met uw zaken in gesprek te gaan.
* De ervaringen van het geheime voorgeheugen voor een bezoeker binnen een zitting op uw server zodat de veelvoudige API vraag kan worden vermeden, die betere prestaties bereikt.
* Naadloos integreren met Adobe Experience Cloud-producten, zoals Adobe Analytics, Adobe Audience Manager (AAM) en de Experience Cloud ID-service van de server.

## Server Side SDK&#39;s

De [!DNL Adobe Target] SDK-documentatie aan serverzijde helpt u bij de implementatie [!DNL Target] op uw servers in uw taal van keuze.

* [Node.js](node-js/overview.md)
* [Java](java/overview.md)
* [.NET](net/overview.md)
* [Python](python/overview.md)

Doorheen [!DNL Adobe Target]SDK&#39;s aan de serverzijde kunt u:

* Uitvoeren en uitvoeren **markering functie**, **rollouts**, en **A/B-experimenten** om **bijna-nullatentie**.
* Ervaringen bieden over **web**, inclusief **SPA**, en **mobiele kanalen** en niet op een browser **IoT-apparaten (Internet of Dingen)** zoals een aangesloten tv, kiosk of digitaal scherm in de winkel.
* Leveren **Door machines aangedreven gepersonaliseerde ervaringen (ML)** aan een gebruiker, geen kwestie welk kanaal of apparaat de gebruiker met uw zaken in dienst heeft genomen.
* **Naadloos integreren met Adobe Experience Cloud** producten zoals **Adobe Analytics**, **Adobe Audience Manager** en de **Experience Cloud ID-service** aan de serverzijde.

Zie de [Aan de slag](sdk-guides/getting-started/getting-started.md) pagina voor informatie over het gebruik van een eenvoudige functie voor het markeren van functies via [Apparaatbeslissingen](sdk-guides/on-device-decisioning/overview.md).

Bekijk onze [Voorbeeldtoepassingen](sdk-guides/sample-apps/sample-apps.md) om plezier te hebben en te spelen!

## [!DNL Target Recommendations] API&#39;s

Koppeling: [Doel Recommendations API&#39;s](https://developers.adobetarget.com/api/recommendations) en [Adobe Recommendations API-overzicht](../../before-administer/recs-api/overview.md).

Met de Recommendations API&#39;s kunt u programmatisch communiceren met [!DNL Target] aanbevelingen servers. Deze API&#39;s kunnen worden geïntegreerd met een reeks toepassingsstapels om functies uit te voeren die u doorgaans via de [!DNL Target] gebruikersinterface.
