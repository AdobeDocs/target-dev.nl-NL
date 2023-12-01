---
title: Overzicht van Adobe Target Profile API's
description: Leer hoe u API's met Adobe Target-profielen kunt gebruiken om bezoekersgegevens te verzenden naar [!DNL Target].
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
source-git-commit: af9db32d59bdf32f2b9fade267922803250377dd
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# [!DNL Adobe Target Profile APIs overview]

Een gebruikersprofiel bevat demografische en gedragsinformatie van een bezoeker van een webpagina, zoals leeftijd, geslacht, aangekochte producten, laatste bezoektijd, enzovoort. [!DNL Adobe Target] gebruikt deze informatie om de inhoud aan te passen die het voor elke bezoeker dient.

De profielgegevens voor elke bezoeker worden opgeslagen in cookies of in apps van derden.

Als uw webpagina de doelcode implementeert ([at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) of de [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk.md)), de profielgegevens van de cookies worden doorgegeven aan [!DNL Target] met profielparameters. [!DNL Target] identificeert elke bezoeker uniek door een `pcID` dat de bezoeker cookies genereert. U kunt profielparameters echter via mbox-aanroepen vanuit een externe toepassing doorgeven met `mbox3rdPartyIds`.

Gebruik de [!DNL Adobe Target] profiel-API&#39;s wanneer u profielgegevens van uw bezoekers kunt verzenden naar [!DNL Target] dat u niet kunt of wilt verzenden als onderdeel van uw op pagina&#39;s gebaseerde integratie met [!DNL Target]. Dit kunnen gegevens zijn van een systeem van het Beheer van de Verhouding van de Klant (CRM) of van het Punt van de Verkoop (POS) dat niet beschikbaar op de pagina, of gegevens van een gevoeliger aard is die geen nut hebben om op de pagina over te gaan.

Er zijn twee manieren om profielen bij te werken via API:

* [API voor bijwerken van één profiel](/help/dev/administer/profile-api/profile-single-api.md)
* [Bulkprofielupdate via batch](/help/dev/administer/profile-api/profile-bulk-api.md)
