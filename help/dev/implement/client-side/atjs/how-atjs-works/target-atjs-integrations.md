---
keywords: at.js-integratie, ondersteunde integratie, niet-ondersteunde integratie, integratie van derden
description: Bekijk de door [!DNL Adobe Target] at.js, inclusief [!UICONTROL Analytics for Target] (A4T) [!UICONTROL Experience Cloud ID Service]en meer.
title: Welke integraties worden door at.js ondersteund?
feature: at.js
exl-id: d2c61e77-5fc7-4c35-905b-76b8c4f9df4b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# at.js-integratie

Informatie over gemeenschappelijke integratie met [!DNL Adobe Target] en hun ondersteuningsstatus met at.js.

Neem contact op met uw accountvertegenwoordiger of consultant als u een dwingende behoefte hebt aan integratie die hier niet wordt ondersteund of vermeld.

## Ondersteunde integratie

| Integratie | Details |
|--- |--- |
| [!UICONTROL Analytics for Target] (A4T) | Zie [Adobe Analytics als rapportagebron voor Adobe Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=nl-NL). |
| [!UICONTROL Profiles & Audiences] (P&amp;A) | Zie [Soorten publiek](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=nl-NL) in de *Gebruikershandleiding voor Core Services*. |
| [!UICONTROL Experience Cloud ID Service] | Zie de [Documentatie Adobe Experience Cloud ID Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=nl-NL). |
| [!UICONTROL Tags in Adobe Experience Platform] | [!UICONTROL Tags in Adobe Experience Platform] zijn de volgende generatie mogelijkheden voor tagbeheer van [!DNL Adobe]. [!UICONTROL Tags] klanten een eenvoudige manier geven om de analytische, marketing- en advertentietags die nodig zijn, te implementeren en te beheren om de relevante ervaringen van klanten te verbeteren. Zie [Implementeren [!DNL Target] gebruiken, Adobe Experience Platform](../how-to-deployatjs/implement-target-using-adobe-launch.md). |
| [!UICONTROL Adobe Experience Manager] (AEM) Cloud Service | De [!UICONTROL AEM Cloud Service] maakt het mogelijk [!UICONTROL A/B Test] en [!UICONTROL Experience Targeting] activiteiten binnen de AEM. Ondersteunt at.js met [!UICONTROL Adobe Experience Manager] 6.2 met FP-11577 (of later). Zie voor meer informatie [Integreren met [!DNL Adobe Target]](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=nl-NL) en selecteer uw AEM. |
| [!UICONTROL AEM Experience Fragments] | Ervaar fragmenten die zijn gemaakt in AEM in [!DNL Target] Met deze activiteiten kunt u het gebruiksgemak en de kracht van AEM combineren met krachtige mogelijkheden voor Automated Intelligence (AI) en Machine Learning (ML) in [!DNL Target] om ervaringen op schaal te testen en te personaliseren.  AEM brengt al uw inhoud en middelen in een centrale plaats samen om uw verpersoonlijkingsstrategie te voeden. Met AEM kunt u eenvoudig inhoud voor desktops, tablets en mobiele apparaten op één locatie maken zonder dat u code hoeft te schrijven. Het is niet nodig om pagina&#39;s te maken voor elk apparaat—AEM past automatisch elke ervaring aan met uw inhoud.  Zie [AEM ervaren fragmenten](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html?lang=nl-NL). |

## Niet-ondersteunde integratie

| Integratie | Details |
|--- |--- |
| Verouderd [!DNL Target] tot [!DNL SiteCatalyst] Integratie | Dit was de integratie die campagne- en recept-id&#39;s naar [!DNL SiteCatalyst] via het paginagesprek zodat u rapporten kunt uitvoeren in het dialoogvenster [!DNL SiteCatalyst] UI. Deze functionaliteit wordt vervangen door A4T. |
| Verouderd [!DNL Target] tot [!DNL SiteCatalyst] Integratie | Dit was de integratie die mbox vraag genoemd maakte `"SiteCatalyst: Event"` en `"SiteCatalyst: Purchase"` zodat u succesmetriek en gebruikersprofielen kon bouwen die op gebeurtenissen en steunen worden gebaseerd. Deze functionaliteit wordt vervangen door A4T en P&amp;A. |
| Verouderd [!DNL Audience Manager] AAM [!DNL Target] Integratie | Dit was de integratie die een front-end API vraag maakte om AAM segmenten terug te winnen en hen toen als mbox parameters op elke mbox vraag op de pagina verzond. |

## Integraties van derden

| Integratie | Details |
|--- |--- |
| Andere tagmanagers | at.js zou met niet-Adobe markeringsbeheerplatforms moeten werken, maar ben zorgvuldig het gebruiken van de eigenschappen van de douaneintegratie die andere verkopers hebben ontwikkeld. Hun integratie zou van interne mbox.js functies afhankelijk kunnen zijn die niet meer in at.js bestaan. |
| Externe gegevensleveranciers (bv. Demandbase, Bluekai, weer-API&#39;s) | Veel gegevensproviders van derden die worden gebruikt als aanvulling op de gebruikerprofilering van Target, kunnen worden geïntegreerd met behulp van at.js [Gegevensleveranciers](../atjs-functions/targetglobalsettings.md#data-providers) gebruiken. |
