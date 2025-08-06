---
title: Profielen bijwerken
description: Leer hoe u API's met Adobe Target-profielen gebruikt om bezoekersgegevens te verzenden naar  [!DNL Target] .
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
source-git-commit: 3b0bc0b67800ed4b1da6ba2bfa05c677147a78ba
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# Profielen bijwerken

Een gebruikersprofiel bevat demografische en gedragsinformatie van een bezoeker van een webpagina, zoals leeftijd, geslacht, aangekochte producten, laatste bezoektijd, enzovoort. [!DNL Adobe Target] gebruikt deze informatie om de inhoud aan te passen die het voor elke bezoeker dient.

De profielgegevens voor elke bezoeker worden opgeslagen in cookies of in apps van derden.

Als uw Web-pagina de [!DNL Target] code ([ at.js ](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md) of [ SDK van het Web van Adobe Experience Platform ](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)) uitvoert, wordt de profielinformatie van de koekjes overgegaan tot [!DNL Target] gebruikend profielparameters. [!DNL Target] identificeert elke bezoeker op unieke wijze via een `pcID` die deze in de cookies van de bezoeker genereert. U kunt profielparameters echter via mbox-aanroepen vanuit een externe toepassing doorgeven met `mbox3rdPartyIds` .

Gebruik de [!DNL Adobe Target] -profiel-API&#39;s wanneer u profielgegevens over uw bezoekers naar [!DNL Target] wilt verzenden die u niet kunt of wilt verzenden als onderdeel van de op pagina&#39;s gebaseerde integratie met [!DNL Target] . Dit kunnen gegevens zijn van een systeem van het Beheer van de Verhouding van de Klant (CRM) of van het verkooppunt (POS) dat niet beschikbaar op de pagina is. Of deze gegevens zijn wellicht gevoeliger en het heeft geen zin de pagina door te geven.

Er zijn twee manieren om profielen bij te werken via API:

* [API voor bijwerken van één profiel](/help/dev/administer/profile-api/profile-single-api.md)
* [Bulkprofielupdate via batch](/help/dev/administer/profile-api/profile-bulk-api.md)
