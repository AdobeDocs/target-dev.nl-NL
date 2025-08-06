---
keywords: implementeren, implementeren, at.js, adobe Experience platform web sdk, aep web sdk
description: Leer hoe te om  [!DNL Adobe Target]  voor cliënt-zijWeb uit te voeren gebruikend  [!DNL Adobe Experience Platform Web SDK]  (het Web SDK van AEP) of de bibliotheek van JavaScript at.js.
title: Hoe voer ik  [!DNL Target]  voor Cliënt-Kant Web uit
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
source-git-commit: 7e2f1620c839393051432485192a45ddda2390a0
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Overzicht: implementeren [!DNL Target] voor web op de client

In een client-side implementatie van [!DNL Adobe Target] levert [!DNL Target] de ervaringen die aan een activiteit zijn gekoppeld rechtstreeks aan de clientbrowser. De browser bepaalt welke ervaring wordt weergegeven en geeft deze weer. Met een cliënt-zijimplementatie, kunt u een redacteur van WYSIWYG, de [ Visuele Composer van de Ervaring ](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=nl-NL) (VEC), of een niet-visuele interface, de [ Op vorm-gebaseerde Composer van de Ervaring ](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=nl-NL) gebruiken, om uw activiteit en verpersoonlijkingservaringen tot stand te brengen.

Als u [!DNL Target] client-side wilt implementeren, moet u een van de volgende JavaScript-bibliotheken gebruiken:

* [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)

  Met [!UICONTROL Adobe Experience Platform Web SDK] kunt u via [!DNL Adobe Experience Cloud] communiceren met de verschillende services in de [!DNL Target] (inclusief [!UICONTROL Adobe Experience Edge Network] ). Als u verkiest om aan [!UICONTROL Adobe Experience Platform Web SDK] te migreren, zie [ wat is [!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md).

* [[!DNL Target] at.js JavaScript-bibliotheek](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)

  De JavaScript-bibliotheek at.js verbetert de laadtijden van pagina&#39;s voor webimplementaties, verbetert de beveiliging en biedt betere implementatieopties voor toepassingen op één pagina. Als u verkiest om aan at.js te migreren, zie [ How At.js werkt ](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) en [[!DNL Adobe Target]  de Bouwer van de Vaardigheid: Het praatje van de ontwikkelaar, migreer Adobe Target mbox.js aan at.js ](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true).


Zie [ het Vergelijken van de bibliotheek at.js aan het Web SDK ](/help/dev/implement/client-side/aep-web-sdk/web-sdk-atjs-comparison.md) om over de verschillen tussen de twee implementatiebenaderingen te leren.