---
keywords: implementeren, implementeren, at.js, adobe Experience platform web sdk, aep web sdk
description: Leer hoe u implementeert [!DNL Adobe Target] voor client-side web met de [!DNL Adobe Experience Platform Web SDK] (AEP Web SDK) of de JavaScript-bibliotheek at.js.
title: Hoe implementeren [!DNL Target] voor Client-Side Web
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
source-git-commit: 2d2a593df661c7e6c6e6384af6042e8aa4575fdb
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Overzicht: implementeren [!DNL Target] voor client-side web

Bij een clientimplementatie van [!DNL Adobe Target], [!DNL Target] levert de ervaringen verbonden aan een activiteit rechtstreeks aan cliëntbrowser. De browser bepaalt welke ervaring wordt weergegeven en geeft deze weer. Met een cliënt-zijimplementatie, kunt u een redacteur gebruiken WYSIWYG, [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=nl-NL) (VEC) of een niet-visuele interface [Form-based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=nl-NL), om uw activiteiten en personalisatie-ervaringen te creëren.

Om [!DNL Target] aan clientzijde moet u een van de volgende JavaScript-bibliotheken gebruiken:

* [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk.md)

  De [!UICONTROL Adobe Experience Platform Web SDK] biedt u de mogelijkheid om te communiceren met de verschillende services in de [!DNL Adobe Experience Cloud] (inclusief [!DNL Target]) via de [!UICONTROL Adobe Experience Edge Network]. Als u naar de [!UICONTROL Adobe Experience Platform Web SDK], zie [Wat is [!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk.md).

* [[!DNL Target] at.js JavaScript-bibliotheek](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md)

  De JavaScript-bibliotheek at.js verbetert de laadtijden van pagina&#39;s voor webimplementaties, verbetert de beveiliging en biedt betere implementatieopties voor toepassingen op één pagina. Als u naar at.js wilt migreren, raadpleegt u [Hoe werkt At.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) en [[!DNL Adobe Target] Skill Builder: chatten met ontwikkelaars, migreren Adobe Target mbox.js naar at.js](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true).


Zie [Het vergelijken van de bibliotheek at.js met het Web SDK](https://experienceleague.adobe.com/nl/docs/experience-platform/web-sdk/personalization/adobe-target/web-sdk-atjs-comparison){target=_blank} kennis te nemen van de verschillen tussen de twee uitvoeringsmethoden .