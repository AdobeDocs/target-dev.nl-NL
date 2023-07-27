---
keywords: implementeren, implementeren, instellen, instellen, paginaparameter, tomcat, url-gecodeerd, in-page profile-kenmerk, mbox-parameter, in-page profielkenmerken, scriptprofielkenmerk, bulkprofielupdate-API, single file update-API, klantkenmerken, Implementeren5, implementeren6, implementeren7, implementeren8, implementeren9, implementatie0, implementatie1, implementatie2, implementatie3, implementatie4, implementatie5, gegevensproviders, gegevensaanbieder
description: Gegevens ophalen in [!DNL Target] (paginaparameters, profielkenmerken, scriptprofielkenmerken, gegevensproviders, API's voor één en één bulkprofielupdate, klantkenmerken).
title: Hoe krijg ik gegevens in het doel?
feature: Implementation
exl-id: a54e306a-ea8e-4d3f-bc5d-b5895b6b9a84
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Overzicht van methoden

Informatie over de verschillende methoden die u kunt gebruiken om gegevens in Adobe Target op te halen.

Beschikbare methoden zijn:

| Methode | Details |
| --- | --- |
| [Paginaparameters](page-parameters.md)<br />(Wordt ook wel &quot;parameters mbox&quot; genoemd) | Paginaparameters zijn naam-/waardeparen die rechtstreeks via paginacode worden doorgegeven en die niet in het profiel van de bezoeker zijn opgeslagen voor toekomstig gebruik.<br />Paginaparameters zijn handig voor het verzenden van paginagegevens naar [!DNL Target] dat niet hoeft te worden opgeslagen met het profiel van de bezoeker voor toekomstig doelgericht gebruik. Deze waarden worden in plaats daarvan gebruikt om de pagina of de actie te beschrijven die de gebruiker op de specifieke pagina heeft ondernomen. |
| [Profielkenmerken in pagina](in-page-profile-attributes.md)<br />(Wordt ook wel &#39;&#39;in-mbox-profielkenmerken&#39; genoemd) | Profielkenmerken in pagina zijn naam-/waardeparen die rechtstreeks door paginacode worden doorgegeven en die in het profiel van de bezoeker worden opgeslagen voor toekomstig gebruik.<br />Met profielkenmerken van pagina&#39;s kunnen gebruikersspecifieke gegevens in het doelprofiel worden opgeslagen, zodat deze later kunnen worden toegewezen en gesegmenteerd. |
| [Scriptprofielkenmerken](script-profile-attributes.md) | Scriptprofielkenmerken zijn naam-/waardeparen die zijn gedefinieerd in het dialoogvenster [!DNL Target] oplossing. De waarde wordt bepaald door het uitvoeren van een JavaScript-fragment op de server van Target per serveraanroep.<br />Gebruikers schrijven kleine codefragmenten die per mbox vraag uitvoeren, en alvorens een bezoeker voor publiek en activiteitenlidmaatschap wordt geëvalueerd. |
| [Gegevensleveranciers](data-providers.md) | Met gegevensproviders kunt u eenvoudig gegevens van derden aan Target doorgeven. |
| [Bulkprofielupdate-API](bulk-profile-update-api.md) | Via API kunt u een .csv-bestand verzenden naar [!DNL Target] met updates voor bezoekersprofielen voor veel bezoekers. Elk bezoekersprofiel kan met veelvoudige in-pagina profielattributen in één vraag worden bijgewerkt. |
| [API voor bijwerken van één profiel](single-profile-update-api.md) | Bijna identiek aan de API voor het bijwerken van het bulkprofiel, maar één bezoekersprofiel wordt tegelijk bijgewerkt, in lijn in de API-aanroep in plaats van met een .csv-bestand. |
| [Klantkenmerken](customer-attributes.md) | Met klantkenmerken kunt u gegevens van bezoekersprofielen uploaden via FTP naar de Experience Cloud. Gebruik de gegevens in Adobe Analytics en Adobe Target nadat ze zijn geüpload. |
