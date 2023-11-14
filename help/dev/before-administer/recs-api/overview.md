---
title: Wat is de Adobe Recommendations API?
description: Deze gids begeleidt ontwikkelaars door hands-on praktijk gebruikend Adobe Target Recommendations APIs om de catalogi van Recommendations en douanecriteria te vormen en te beheren, evenals het gebruiken van levering API om aanbevelingen inhoud terug te winnen.
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 0d03c650-0b00-44b8-a794-10e5d738e42c
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Overzicht Adobe Recommendations API

API&#39;s die relevant zijn voor Recommendations-include-bestanden [Admin API&#39;s](../../before-administer/target-api-overview.md) dat u in staat stelt:

* Uw catalogus met aanbevolen producten of inhoud beheren
* Uw Recommendations-algoritmen en -activiteiten beheren

Het doel gebruiken [Leverings-API](../../implement/delivery-api/overview.md) Met Recommendations kunt u ook:

* U kunt aanbevelingen ophalen in JSON-, HTML- of XML-objecten, zodat deze kunnen worden weergegeven in web, mobiel, e-mail, internet van dingen (IOT) en andere kanalen.

## Beschrijving

In deze handleiding met betrekking tot de Recommendations API&#39;s worden ontwikkelaars door de praktijk geleid die de Recommendations API&#39;s gebruikt om Recommendations-catalogi en aangepaste criteria te configureren en te beheren, en met behulp van de Delivery API aanbevolen inhoud op te halen. Tegen het einde kunt u het volgende doen:

* Entiteiten configureren en beheren met de Recommendations API
* Aangepaste criteria configureren en beheren met de Recommendations API
* Begrijp hoe u Recommendations met de bezorgings-API kunt gebruiken om aanbevelingen te gebruiken die resulteren in niet-HTML-apparaten

## Publiek

Deze handleiding is bedoeld voor ontwikkelaars die niet bekend zijn met doel-API&#39;s of Recommendations API&#39;s.

## Vereisten {#prerequisites}

De API&#39;s voor doelbeheer zijn vereist [Instellingen voor verificatie van Adoben](../configure-authentication.md). Zorg ervoor dat dit is geconfigureerd voordat u de Recommendations API gebruikt.

## Bronnen

Neem nota van de volgende middelen, die noodzakelijk zijn om deze gids te begrijpen en het met succes te volgen:

| Bron | Details |
| --- | --- |
| Postman | Krijg de [Postman-app](https://www.postman.com/downloads/) voor uw besturingssysteem. Postman basic is gratis bij het maken van accounts. Hoewel Postman niet vereist is voor het gebruik van Adobe Target API&#39;s in het algemeen, maakt het API-workflows eenvoudiger en biedt Adobe Target verschillende Postman-verzamelingen om de API&#39;s van uit te voeren en te leren hoe ze werken. Voor de rest van deze handleiding wordt uitgegaan van praktische kennis van Postman. Raadpleeg voor hulp de [Postman-documentatie](https://learning.getpostman.com/). |
| Verwijzingen | In de rest van deze handleiding wordt ervan uitgegaan dat de volgende bronnen bekend zijn:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentatie voor Admin en Profile API](../../administer/admin-api/admin-api-overview-new.md)</li><li>[Recommendations API-documentatie](https://developer.adobe.com/target/administer/recommendations-api/)</li></UL> |
