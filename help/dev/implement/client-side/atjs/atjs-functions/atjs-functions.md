---
keywords: at.js, functies, javascript-bibliotheek
description: Bekijk een lijst van functies die met de 1.x en 2.x versies van de at.js JavaScript bibliotheek in  [!DNL Adobe Target] kunnen worden gebruikt.
title: Welke functies kan ik gebruiken met at.js?
feature: at.js
exl-id: 1efed365-8a74-4c85-bdb1-8daaaf53d642
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# at.js-functies

Lijst met functies die kunnen worden gebruikt met de JavaScript-bibliotheek [!DNL Adobe Target] at.js. Klik op de koppelingen in de kolom Functie voor meer informatie en voorbeelden.

| Functie | Details |
| --- | --- |
| [[!UICONTROL adobe.target.getOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) | Deze functie voert een aanvraag in om een [!DNL Target] -aanbieding te krijgen. Gebruik deze methode met `adobe.target.applyOffer()` om de reactie te verwerken of gebruik uw eigen succesafhandeling. |
| [[!UICONTROL adobe.target.getOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)<P>(om 2.x.js) | Deze functie laat u veelvoudige aanbiedingen terugwinnen door in veelvoudige dozen over te gaan. Bovendien kunnen meerdere aanbiedingen worden opgehaald voor alle weergaven in actieve activiteiten.<P>**Nota:** Deze functie werd geïntroduceerd met at.js 2.x. Deze functie is niet beschikbaar voor versie 1 van at.js.*x*. |
| [[!UICONTROL adobe.target.applyOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) | Deze functie is bedoeld voor het toepassen van de inhoud van de reactie. |
| [[!UICONTROL adobe.target.applyOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)<P>(om 2.x.js) | Met deze functie kunt u meerdere aanbiedingen toepassen die zijn opgehaald door [!UICONTROL adobe.target.getOffers()] .<P>**Nota:** Deze functie werd geïntroduceerd met at.js 2.x. Deze functie is niet beschikbaar voor versie 1 van at.js.*x*. |
| [[!UICONTROL adobe.target.triggerView (viewName, options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)<P>(om 2.x.js) | Deze functie kan worden aangeroepen wanneer een nieuwe pagina wordt geladen of wanneer een component op een pagina opnieuw wordt weergegeven.<P> Deze functie moet worden geïmplementeerd voor toepassingen op één pagina (SPA&#39;s), zodat u [!UICONTROL Visual Experience Composer] (VEC) kunt gebruiken om [!UICONTROL A/B Test] - en [!UICONTROL Experience Targeting] (XT)-activiteiten te maken. |
| [[!UICONTROL adobe.target.trackEvent(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) | Deze functie voert een verzoek in om gebruikersacties, zoals kliks en omzettingen te melden. Het levert geen activiteiten in de reactie. |
| [[!UICONTROL mboxCreate(mbox,params)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)<P>(om 1.js) | Voert een verzoek uit en past de aanbieding op dichtstbijzijnde div met mboxDefault klassennaam toe.<P>**Nota:** Deze functie is beschikbaar voor versies 1 van at.js.*x* slechts. Deze functie is vervangen door de release van at.js 2.x. Deze functie retourneert standaardinhoud als deze wordt gebruikt met at.js 2.x. |
| [[!UICONTROL mboxDefine(options)] en [!UICONTROL mboxUpdate(options)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)<P>(om 1.js) | Een box definiëren en bijwerken.<P>**Nota:** Deze functie is beschikbaar voor versies 1 van at.js.*x* slechts. Deze functie is vervangen door de release van at.js 2.x. Deze functie retourneert standaardinhoud als deze wordt gebruikt met at.js 2.x. |
| [[!UICONTROL targetGlobalSettings(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) | U kunt instellingen in de bibliotheek at.js overschrijven met behulp van `[!UICONTROL targetGlobalSettings()]` in plaats van ze te configureren in de gebruikersinterface van [!DNL Target Standard/Premium] of met behulp van REST API&#39;s.<ul><li>Gegevensleveranciers: Met deze instelling kunnen klanten gegevens verzamelen van externe gegevensleveranciers, zoals Demandbase, BlueKai en aangepaste services, en de gegevens doorgeven aan Target als mbox-parameters in het algemene mbox-verzoek.</li></ul> |
| [[!UICONTROL targetPageParams(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) | Met deze methode kunt u parameters aan de globale mbox koppelen van buiten de aanvraagcode. |
| [[!UICONTROL targetPageParamsAll(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md) | Met deze methode kunt u parameters koppelen aan alle vakken van buiten de aanvraagcode. |
| [[!UICONTROL registerExtension(options)]](/help/dev/implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)<P>(om 1.js) | Verstrekt een standaardmanier om een specifieke uitbreiding te registreren.<P>**Nota:** Deze functie is beschikbaar voor versies 1 van at.js.*x* slechts. Deze functie is vervangen door de release van at.js 2.x. Deze functie retourneert standaardinhoud als deze wordt gebruikt met at.js 2.x. |
| [[!UICONTROL at.js custom events]](/help/dev/implement/client-side/atjs/atjs-functions/atjs-custom-events.md) | op.js laten de douanegebeurtenissen u weten wanneer een mbox- verzoek of een aanbieding ontbreekt of slaagt. |
| [[!UICONTROL adobe.target.sendNotifications(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)<P>(js 2.1.0) | Deze functie verzendt een bericht naar [!DNL Target] edge wanneer een ervaring wordt teruggegeven zonder `[!UICONTROL adobe.target.applyOffer()]` of `[!UICONTROL adobe.target.applyOffers()]` te gebruiken.<P>**Nota**: Deze functie is geïntroduceerd in at.js 2.1.0 en zal voor om het even welke versies boven 2.1.0 beschikbaar zijn. |
