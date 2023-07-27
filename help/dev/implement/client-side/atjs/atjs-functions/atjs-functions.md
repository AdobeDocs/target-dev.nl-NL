---
keywords: at.js, functies, javascript-bibliotheek
description: Een lijst weergeven met functies die kunnen worden gebruikt met de 1.x- en 2.x-versies van de JavaScript-bibliotheek at.js in [!DNL Adobe Target].
title: Welke functies kan ik gebruiken met at.js?
feature: at.js
exl-id: 1efed365-8a74-4c85-bdb1-8daaaf53d642
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# at.js-functies

Lijst met functies die kunnen worden gebruikt met de [!DNL Adobe Target] at.js JavaScript-bibliotheek. Klik op de koppelingen in de kolom Functie voor meer informatie en voorbeelden.

| -functie | Details |
| --- | --- | 
| [[!UICONTROL adobe.target.getOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) | Deze functie activeert een verzoek om een [!DNL Target] voorstel. Gebruiken met `adobe.target.applyOffer()` om de reactie te verwerken of uw eigen succesafhandeling te gebruiken. |
| [[!UICONTROL adobe.target.getOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)<P>(om 2.x.js) | Deze functie laat u veelvoudige aanbiedingen terugwinnen door in veelvoudige dozen over te gaan. Bovendien kunnen meerdere aanbiedingen worden opgehaald voor alle weergaven in actieve activiteiten.<P>**Opmerking:** Deze functie is geïntroduceerd met at.js 2.x. Deze functie is niet beschikbaar voor versie 1 van at.js.*x*. |
| [[!UICONTROL adobe.target.applyOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) | Deze functie is bedoeld voor het toepassen van de inhoud van de reactie. |
| [[!UICONTROL adobe.target.applyOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)<P>(om 2.x.js) | Met deze functie kunt u meerdere aanbiedingen toepassen die zijn opgehaald door [!UICONTROL adobe.target.getOffers()].<P>**Opmerking:** Deze functie is geïntroduceerd met at.js 2.x. Deze functie is niet beschikbaar voor versie 1 van at.js.*x*. |
| [[!UICONTROL adobe.target.triggerView (viewName, options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)<P>(om 2.x.js) | Deze functie kan worden aangeroepen wanneer een nieuwe pagina wordt geladen of wanneer een component op een pagina opnieuw wordt weergegeven.<P> Deze functie moet worden geïmplementeerd voor toepassingen van één pagina (SPA) om de functie [!UICONTROL Visual Experience Composer] (VEC) om [!UICONTROL A/B Test] en [!UICONTROL Experience Targeting] (XT) activiteiten. |
| [[!UICONTROL adobe.target.trackEvent(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) | Deze functie voert een verzoek in om gebruikersacties, zoals kliks en omzettingen te melden. Het levert geen activiteiten in de reactie. |
| [[!UICONTROL mboxCreate(mbox,params)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)<P>(om 1.js) | Voert een verzoek uit en past de aanbieding op dichtstbijzijnde div met mboxDefault klassennaam toe.<P>**Opmerking:** Deze functie is beschikbaar voor at.js versies 1.*x* alleen. Deze functie is vervangen door de release van at.js 2.x. Deze functie retourneert standaardinhoud als deze wordt gebruikt met at.js 2.x. |
| [[!UICONTROL mboxDefine(options)] en [!UICONTROL mboxUpdate(options)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)<P>(om 1.js) | Een box definiëren en bijwerken.<P>**Opmerking:** Deze functie is beschikbaar voor at.js versies 1.*x* alleen. Deze functie is vervangen door de release van at.js 2.x. Deze functie retourneert standaardinhoud als deze wordt gebruikt met at.js 2.x. |
| [[!UICONTROL targetGlobalSettings(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) | U kunt instellingen in de bibliotheek at.js overschrijven met `[!UICONTROL targetGlobalSettings()]`, in plaats van deze in de [!DNL Target Standard/Premium] UI of via REST API&#39;s.<ul><li>Gegevensleveranciers: Met deze instelling kunnen klanten gegevens verzamelen van externe gegevensleveranciers, zoals Demandbase, BlueKai en aangepaste services, en de gegevens doorgeven aan Target als mbox-parameters in het algemene mbox-verzoek.</li></ul> |
| [[!UICONTROL targetPageParams(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) | Met deze methode kunt u parameters aan de globale mbox koppelen van buiten de aanvraagcode. |
| [[!UICONTROL targetPageParamsAll(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md) | Met deze methode kunt u parameters koppelen aan alle vakken van buiten de aanvraagcode. |
| [[!UICONTROL registerExtension(options)]](/help/dev/implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)<P>(om 1.js) | Verstrekt een standaardmanier om een specifieke uitbreiding te registreren.<P>**Opmerking:** Deze functie is beschikbaar voor at.js versies 1.*x* alleen. Deze functie is vervangen door de release van at.js 2.x. Deze functie retourneert standaardinhoud als deze wordt gebruikt met at.js 2.x. |
| [[!UICONTROL at.js custom events]](/help/dev/implement/client-side/atjs/atjs-functions/atjs-custom-events.md) | op.js laten de douanegebeurtenissen u weten wanneer een mbox- verzoek of een aanbieding ontbreekt of slaagt. |
| [[!UICONTROL adobe.target.sendNotifications(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)<P>(js 2.1.0) | Deze functie verzendt een bericht naar [!DNL Target] rand wanneer een ervaring zonder het gebruiken wordt teruggegeven `[!UICONTROL adobe.target.applyOffer()]` of `[!UICONTROL adobe.target.applyOffers()]`.<P>**Opmerking**: Deze functie is geïntroduceerd in at.js 2.1.0 en is beschikbaar voor versies boven 2.1.0. |
