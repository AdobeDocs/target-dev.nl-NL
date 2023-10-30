---
keywords: at.js-releases, at.js-versies, releaseopmerkingen
description: Bekijk de details over wijzigingen in elke versie van het dialoogvenster [!DNL Adobe Target] at.js JavaScript-bibliotheek.
title: Wat is inbegrepen in Elke Versie van at.js?
feature: at.js
exl-id: 609dacba-2ab8-45e9-b189-928d59938c98
source-git-commit: c5d1f477a2561a59efb3250e35563b48822fbe59
workflow-type: tm+mt
source-wordcount: '4674'
ht-degree: 0%

---

# details at.js-versie

Details over de wijzigingen in elke versie van het dialoogvenster [!DNL Adobe Target] at.js JavaScript-bibliotheek.

>[!IMPORTANT]
>
>[!DNL Adobe Target] ondersteunt beide at.js 1.*x* en te.js 2.*x*.
>
>te.js 1.*x* is in de onderhoudsmodus gegaan. De [!DNL Target] teamreleases foutoplossingen en beveiligingspatches indien nodig.
>
>De [!DNL Target] team biedt volledige ondersteuning voor at.js 2.*x* en geeft oplossingen voor problemen, beveiligingspatches, functies en optimalisatie van prestaties voortdurend weer.
>
>U zou aan de recentste versies van één van beide moeten bevorderen 1.*x* of 2.*x* om insectenmoeilijke situaties en veiligheidspatches voor kwesties te verkrijgen die in om het even welke vorige minder belangrijke versie van de overeenkomstige belangrijkste versie worden ontdekt.

Tags in [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) zijn de aangewezen methode om at.js te bevorderen. Extensieontwikkelaars voegen voortdurend nieuwe functies toe aan hun extensies en corrigeren vaak bugs. Deze updates worden verpakt in nieuwe versies van een extensie en worden als upgrades beschikbaar gesteld in de Adobe Experience Platform-catalogus. Zie voor meer informatie [Uitbreidingen upgraden](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/extensions/extension-upgrade.html) in de *Overzicht van codes* guide.6+

## at.js versie 2.11.2 (26 oktober 2023)

* Probleem verholpen die inconsistenties veroorzaakte in reactie op tokens die werden verzonden op aangepaste gebeurtenissen.

## at.js versie 2.11.1 (13 oktober 2023)

* Probleem verholpen waarbij niet-afgevangen fouten werden veroorzaakt terwijl een pagina die op.js wordt uitgevoerd, zich in de modus Kirken bevindt.

## at.js versie 2.11.0 (10 oktober 2023)

* Extra ondersteuning voor het instellen van aangepaste [!DNL Adobe Experience Platform] (AEP) `sandboxId` en `sandboxName` in `targetGlobalSettings`, die wordt doorgegeven aan de API voor levering op `getOffer/getOffers` oproepen.
* Schaduw-DOM-correctie voor ketting `:eq()` in kiezers.

## at.js versie 2.10.3 (12 september 2023)

* Probleem verholpen waarbij de fout `at-content-rendering-succeeded` aangepaste gebeurtenis wanneer geen aanbiedingen worden weergegeven. De juiste gebeurtenis, `at-content-rendering-no-offers`, wordt nu geactiveerd.
* Toegevoegd `eventToken` en `responseTokens` aan foutobject voor de `at-content-rendering-failed` aangepaste gebeurtenis.

## at.js versie 2.10.2 (7 maart 2023)

* Het probleem dat de oorzaak was van de `trackEvent` om altijd een fout te retourneren.

## at.js versie 2.10.1 (2 februari 2023)

* Probleem verholpen waarbij activiteiten waarbij publieksregels betrokken waren die parameters met punten in hun namen bevatten, niet de verwachte ervaring retourneren, voor het bepalen van het apparaat.
* Oplossing van een bug die in at.js 2.6.0 werd geïntroduceerd waarin at.js een leveringsvraag vuurde, zelfs wanneer mboxDisable werd toegelaten.

## at.js versie 2.10.0 (19 september 2022)

* Extra ondersteuning voor cookies van derden.

## at.js versie 2.9.0 (27 mei 2022)

* Toegevoegd [Clienttips van gebruikersagent](user-agent-and-client-hints.md) ondersteuning.
* Probleem verholpen waarbij meerdere mbox-aanvragen op dezelfde pagina verschillende beeld-id&#39;s hebben.

## at.js versie 2.8.1 (28 januari 2022)

* Vast `pageLoad` wordt niet toegewezen aan target-global-mbox in de hybride uitvoeringsmodus van On Device Decisioning (ODD).
* Probleem verholpen met analytische details voor mbox-aanvraag.
* Verbeterde dev-afhankelijkheden om beveiligingsproblemen te verhelpen.

## at.js versie 2.8.0 (7 januari 2022)

De [!DNL Target] in de JavaScript-bibliotheek at.js worden nu gegevens over het gebruik van functies en de prestaties van telemetriegegevens verzameld. Persoonlijke gegevens worden niet verzameld. Afmelden voor deze functie is beschikbaar door de instelling `telemetryEnabled` naar false in `targetGlobalSettings`. Zie voor meer informatie [telemetryEnabled in targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#telemetryenabled).

## at.js versie 2.7.0 (28 oktober 2021)

Deze release bevat de volgende verbeteringen:

* Extra ondersteuning voor [Webcomponenten](https://developer.mozilla.org/en-US/docs/Web/Web_Components). Deze versie van at.js wordt vereist om gepersonaliseerde ervaringen en aanbiedingen op douaneelementen en op elementen binnen douaneelementen tot stand te brengen en te testen. Deze functionaliteit is opgenomen in de [!DNL Target Standard/Premium] Release 21.10.5.

## om 1.8.3 uur (21 september 2021)

Deze release bevat de volgende wijzigingen:

* De `reactor-window` en `reactor-document` Adobe Experience Platform Launch modules om ervoor te zorgen dat de Platform launch correct functioneert voor klanten die hebben `window.default` of `document-default` set.
* at.js 1.8.3 wordt nu expliciet ingesteld `Samesite=None` en `Secure` om ervoor te zorgen dat cookies van derden correct worden ingesteld.

## om 2.6.1.2021 (16 augustus 2021)

* Bugcorrectie voor &quot;Geen artefact in cache beschikbaar voor hybride modus&quot; bij gebruik van apparaatbeslissingen.

## om 2.6.0 uur (16 juli 2021)

* Veilig kenmerk toegevoegd aan cookies wanneer instellingen at.js `secureOnly` is ingesteld op `true`.
* Reactietokens zijn nu beschikbaar bij gebruik `triggerView()`.
* Probleem verholpen met betrekking tot de `CONTENT_RENDERING_NO_OFFERS` gebeurtenis. Deze gebeurtenis wordt nu correct geactiveerd wanneer er geen inhoud wordt geretourneerd van [!DNL Target].
* [!UICONTROL Analytics for Target] (A4T) klik metriekdetails correct zijn teruggekeerd wanneer het gebruiken `prefetch` verzoeken.
* UUID-generatie wordt niet langer gebruikt `Math.random()`, maar vertrouwt op `window.crypto`.
* De `sessionId` de vervaldatum van het koekje wordt correct uitgebreid op elke netwerkvraag.
* De initialisatie van de weergavecache Single Page Application (SPA) wordt nu correct afgehandeld en wordt gerespecteerd `viewsEnabled` instellingen. Instelling `viewsEnabled` aan de `false` waarde schakelt nu de optie `triggerView()` functie. Zie [Volgorde van bewerkingen voor het laden van de eerste pagina](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md#order).

## om 2.5.0 uur (13 mei 2021)

Deze versie van at.js bevat de volgende verbeteringen en wijzigingen:

* [Apparaatbeslissingen](/help/dev/implement/client-side/atjs/on-device-decisioning/on-device-decisioning.md) ondersteuning voor at.js.
* [Koppelingen voorvertonen](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) ondersteuning van Automated Personalization-activiteiten

Deze release verwijdert ook ondersteuning voor Microsoft Internet Explorer 10 en hoger.

## om 2.4.1.2021 (23 maart 2021)

Deze versie van at.js is een onderhoudsrelease en bevat de volgende verbeteringen en oplossingen:

* Probleem opgelost met `targetPageParams` worden opgenomen in mbox-aanvragen. `targetPageParams` dient te worden opgenomen in `pageLoad` alleen aanvragen. (TNT-40247)
* Geoptimaliseerde venster- en documentglobals die verwijzen in de Adobe Experience Platform-extensie. (TNT-37124)

## om 2.4.0 uur (14 januari 2021)

Deze release van at.js is een onderhoudsrelease en bevat de volgende oplossingen:

* Voegt ondersteuning voor Unified Profile/Platform-id toe aan Delivery API customerIds.
* Oplossing voor een ongeldige inspuiting van stijllabels.

## om 2.3.3.2013 (13 november 2020)

Deze release van at.js is een onderhoudsrelease en bevat de volgende oplossing:

* Correctie van een probleem met betrekking tot het bijhouden van een postvak en A4T. Met 0n-klik, [!DNL Target] Er is een API-aanroep voor levering geactiveerd met de juiste mbox- en mbox-parameters. De SDID komt echter niet overeen met die in het dialoogvenster [!DNL Analytics] de vraag, daarom was er geen klap het stitching en de omschakeling. (TNT-38372)

## te.js 2.3.2 (24 juli 2020)

Deze release van at.js is een onderhoudsrelease en bevat de volgende oplossing:

* Het probleem is opgelost wanneer een script of code een standaardeigenschap aan het venster of document toevoegt.

## om 1.8.2 uur (15 juni 2020)

Deze release van at.js is een onderhoudsrelease en bevat de volgende oplossing:

* Probleem verholpen bij gebruik van CNAME en randoverschrijving, op .js 1.*x* kan het serverdomein onjuist maken, wat tot [!DNL Target] verzoek mislukt. (TNT-35064)

## releases (15 juni 2020)

Deze versie van at.js is een onderhoudsrelease en bevat de volgende verbeteringen en oplossingen:

* De `deviceIdLifetime` overschrijfbaar instellen via [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md). (TNT-36349)
* Probleem verholpen bij gebruik van CNAME en randoverschrijving, op .js 2.*x* kan het serverdomein onjuist maken, wat tot [!DNL Target] verzoek mislukt. (TNT-35065)
* Probleem verholpen tijdens het gebruik van de [!DNL Target] de extensie v2 en de [!UICONTROL Adobe Analytics Launch] extensie, [!DNL Target] de [!DNL Analytics] `sendBeacon` vraag. (TNT-36407, TNT-35990, TNT-36000)

## at.js versie 2.3.0 (25 maart 2020)

Deze versie van at.js is een onderhoudsrelease en bevat de volgende verbeteringen en oplossingen:

* Ondersteuning voor het instellen van Content Security Policy-nonces op SCRIPT- en STYLE-tags die aan het pagina-DOM worden toegevoegd bij het toepassen van de geleverde versie [!DNL Target] voorstellen. Klanten kunnen instellen `targetGlobalSettings.cspScriptNonce` en `targetGlobalSettings.cspStyleNonce` zodat at.js het overeenkomstige script en de stijlmarkering nonces op toegepaste aanbiedingen kan plaatsen. Zie  [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) voor meer informatie .
* Probleem verholpen bij het compileren van at.js met de Google-compiler voor de implementatie van Google-tagbeheer.
* De naam van het selectievakje at.js is gewijzigd in `check` tot `at_check` om botsingen met de implementaties van klanten te vermijden.

## at.js versie 1.8.1 (25 maart 2020)

Deze versie van at.js is een onderhoudsrelease en bevat de volgende verbeteringen en oplossingen:

* De naam van het selectievakje at.js is gewijzigd in `check` tot `at_check` om botsingen met de implementaties van klanten te vermijden.

## at.js versie 2.2.0 (10 oktober 2019)

Deze versie van at.js bevat de volgende verbeteringen en oplossingen:

* Correctie van een probleem waarbij conversies niet werden gerapporteerd door klikken op bijhouden in [!DNL Analytics for Target] (A4T) wanneer [!DNL Adobe Analytics] code was not present on page elements.
* Betere prestaties bij het gebruik van zowel Experience Cloud ID Service (ECID) v4.4 als at.js 2.2 op uw webpagina&#39;s.
* Eerder, maakte ECID twee blokkerende vraag alvorens at.js ervaringen kon halen. Dit is verminderd tot één enkele vraag, die beduidend prestaties verbetert.
* Correctie van foutieve vooraf ingestelde verwerking van weergaven, waarbij tokens voor gebeurtenissen van standaardaanbiedingen niet waren opgenomen in verzonden berichten.

>[!NOTE]
>
>Upgrade de ECID-extensie naar v4.4 om te profiteren van deze prestatieverbetering.

* at.js versie 2.2 verstrekt ook een nieuw die plaatsen genoemd `serverState`. Deze instelling kan worden gebruikt om de paginaprestaties te optimaliseren bij een hybride integratie van [!DNL Target] is geïmplementeerd. Hybride integratie betekent dat u zowel at.js v2.2+ aan de clientzijde als de Delivery-API of een [!DNL Target] SDK aan de serverzijde om ervaringen te bieden. `serverState` geeft at.js v2.2+ de capaciteit om ervaringen direct van inhoud toe te passen die op de server wordt gehaald en aan de cliënt als deel van de pagina teruggegeven wordt. Zie &quot;serverState&quot; in [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverstate).

## at.js versie 1.8.0 (10 oktober 2019)

Deze versie van at.js bevat de volgende verbeteringen en oplossingen:

* Betere prestaties bij het gebruik van zowel Experience Cloud ID Service (ECID) v4.4 als at.js 1.8 op uw webpagina&#39;s.
* Eerder, maakte ECID twee blokkerende vraag alvorens at.js ervaringen kon halen. Dit is verminderd tot één enkele vraag, die beduidend prestaties verbetert.

>[!NOTE]
>
>Upgrade de ECID-extensie naar v4.4 om te profiteren van deze prestatieverbetering.

## at.js versie 2.1.1 (24 juli 2019)

Deze versie van at.js is een onderhoudsrelease en bevat de volgende verbeteringen en oplossingen:

(De uitgiftenummers tussen haakjes zijn bedoeld voor gebruik door een interne Adobe.)

* Oplossing een kwestie die veelvoudige bakens aan brand veroorzaakte toen het gebruiken van de Metrisch van het Volgen van de Klik op de pagina van Doelstellingen &amp; van Montages in Visual Experience Composer (VEC). (TNT-32812)
* Probleem verholpen dat ertoe heeft geleid `triggerView()` om aanbiedingen niet meer dan één keer te renderen. (TNT-32780)
* Probleem opgelost met `triggerView()` om ervoor te zorgen dat het verzoek Marketing Cloud-ID (MCID)-informatie bevat. (TNT-32776)
* Het probleem dat ervoor zorgde dat de `triggerView()` bericht wordt afgevuurd, zelfs als er geen opgeslagen weergaven zijn. (TNT-32614)
* Probleem verholpen die een fout veroorzaakte door het gebruik van de decodeURIcomponent die problemen veroorzaakte wanneer de URL een onjuist gevormde parameter van het vraagkoord bevat. (TNT-32710)
* De bakenvlag wordt nu geplaatst aan &quot;waar&quot;in de context van leveringsverzoeken die via `Navigator.sendBeacon()` API. (TNT-32683)
* Probleem verholpen waarbij Recommendations-aanbiedingen voor een paar klanten niet konden worden weergegeven op websites. Klanten konden de inhoud van de aanbieding zien in de vraag van de leverings-API, maar de aanbieding werd niet toegepast op de website. (TNT-32680)
* Probleem verholpen waarbij klikken-volgen over meerdere ervaringen ertoe leidde dat het programma niet naar behoren functioneerde. (TNT-32644)
* Probleem verholpen waardoor at.js de tweede metrische waarde niet kon toepassen na het renderen van de eerste metrische waarde. (TNT-32628)
* Probleem verholpen bij passeren `mbox3rdPartyId` met de `targetPageParams` functie die ertoe leidde dat de verzoeklading om niet in of de vraagparameters of in de verzoeklading aanwezig was. (TNT-32613)
* Probleem verholpen waardoor de weergave werd geblokkeerd en op reacties op meldingen werd geklikt in browsers op basis van chroom (inclusief Google Chrome). (TNT-32290)

## at.js versie 2.1.0 (3 juni 2019)

Deze release bevat de volgende functies en verbeteringen:

* **Ondersteuning voor Adobe Option-in**: Adobe Opt-In is een manier om de integratie van oplossingen voor Adoben met toestemmingsbeheerplatforms te vereenvoudigen. Voor meer informatie over Adobe Opt-in, zie [Privacy en algemene gegevensbeschermingsverordening (GDPR)](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md).

* **Compatibel met industriestandaard CSP**: at.js gebruikt eval() niet meer om JavaScript uit te voeren.

* **Logboekregistratie voor analyses op de client**: Geef klanten de volledige controle over de manier waarop ze analysegegevens naar [!DNL Adobe Analytics], zowel op de client als op de server.

  Zie voor meer informatie [Client-kant [!DNL Analytics] logboekregistratie](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html#client-side).

* **Meldingen verzenden**: Ontwikkelaars toestaan meldingen te verzenden wanneer een ervaring door hun code wordt gegenereerd in plaats van `applyOffer()` of `applyOffers()`.

  Zie voor meer informatie [adobe.target.sendNotifications(options)](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md).

* **grootte bij.js verminderd met ~24%**: De grootte van at.js wordt verminderd met ~24%. De kleinere bestandsgrootte verbetert de laadprestaties van de pagina en verkort de downloadtijd op .js op de pagina.

## at.js versie 2.0.1 (19 maart 2019)

Dit is een onderhoudrelease met de volgende verbeteringen en oplossingen:

(De uitgiftenummers tussen haakjes zijn bedoeld voor gebruik door een interne Adobe.)

* Probleem verholpen met een zeldzame omstandigheid in de opiniepeilingscode voor DOM die JavaScript-uitzonderingen voor bepaalde klanten veroorzaakte. (TNT-31869)
* Meldingen dat weergaven werden gerenderd, zijn losgekoppeld van gebeurtenishandlers voor het bijhouden van klikken. Aanvankelijk [!DNL Target] heeft geen meldingen verzonden als click-event-handlers die tot een weergegeven weergave behoren, niet konden worden gekoppeld. [!DNL Target] verzendt nu een meningsbericht zelfs wanneer de klikelementen niet worden gevonden. (TNT-31969)
* Probleem verholpen waarbij de omleidingsvlag voor de gebeurtenis die na het verzoek werd uitgevoerd, altijd werd ingesteld op true. (TNT-31907)
* Probleem opgelost dat ertoe leidde dat VEC opnieuw rangschikte actie als succes werd geregistreerd, zelfs wanneer de elementen ontbraken. (TNT-31924)
* Probleem opgelost waarbij meldingen voor bepaalde klanten werden verzonden om de eigenschappentoken voor Enterprise-machtigingen niet te bevatten. (TNT-31999)

## at.js versie 1.7.1 (19 maart 2019)

Dit is een onderhoudrelease met de volgende oplossing:

(De uitgiftenummers tussen haakjes zijn bedoeld voor gebruik door een interne Adobe.)

* Probleem verholpen met een zeldzame omstandigheid in de opiniepeilingscode voor DOM die JavaScript-uitzonderingen voor bepaalde klanten veroorzaakte. (TNT-31869)

## at.js Versie 2.0.0

at.js 2.x verstrekt rijke eigenschapreeksen die uw zaken uitrusten om verpersoonlijking op volgende generatie cliënt-zijtechnologieën uit te voeren. Deze nieuwe versie is gericht op het upgraden van at.js voor harmonieuze interacties met toepassingen van één pagina (SPA).

Hier volgen enkele voordelen van het gebruik van at.js 2.x die niet beschikbaar zijn in eerdere versies:

* De capaciteit om alle aanbiedingen op paginading in het voorgeheugen onder te brengen om veelvoudige servervraag aan één enkele servervraag te verminderen.
* Verbeter de ervaringen van uw eindgebruikers op uw site aanzienlijk, omdat aanbiedingen direct via het cachegeheugen worden weergegeven zonder vertraging die traditionele serveraanroepen introduceren.
* Eenvoudige one-line van code en éénmalige ontwikkelaarsopstelling om uw marketers toe te laten om A/B en de activiteiten van de Ervaring (XT) via Visual Experience Composer (VEC) op uw enige paginatoepassingen tot stand te brengen en in werking te stellen.

at.js 2.x introduceert de volgende nieuwe functies:

* getOffers()
* applyOffers()
* triggerView()

De volgende functies zijn vervangen door de introductie van at.js 2.x:

* mboxCreate()
* mboxDefine
* registerExtension()

Zie voor meer informatie [Bijwerken van at.js 1.x naar at.js 2.x](/help/dev/implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md) en [at.js-functies](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md).

>[!NOTE]
>
>Als u de Adobe-plug-in voor de [Algemene verordening inzake gegevensbescherming](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) (GDPR), moet u momenteel gebruiken om .js 1.7.0 of om .js 2.1.0 of later.

## at.js versie 1.7.0

at.js 1.7.0 biedt ondersteuning voor Adobe Opt-In. Adobe Opt-In is een manier om de integratie van oplossingen voor Adobe met toestemmingsbeheerplatforms te vereenvoudigen.

Voor meer informatie over Adobe Opt-in, zie [Privacy en algemene gegevensbeschermingsverordening](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) (GDPR).

In deze release is ook een probleem opgelost waarbij [!DNL Target] Het is mogelijk dat URL-parameters voor omleiding worden overschreven door parameters die afkomstig zijn van de omleidings-URL.

>[!NOTE]
>
>Als u ondersteuning voor Adobe Opt-in voor GDPR nodig hebt, moet u momenteel at.js 1.7.0 of at.js 2.1.0 of hoger gebruiken.

## at.js Versie 1.6.4

at.js 1.6.4 is een onderhoudsrelease en behandelt het volgende probleem:

* Probleem verholpen waarbij zich in Microsoft Internet Explorer 11 een zeldzame omstandigheid manifesteerde die dubbele aanbiedingen tot gevolg had.

## at.js versie 1.6.3

at.js versie 1.6.3 bevat de volgende correcties en verbeteringen:

* Kiezers hebben nu een CSS-escape-teken als ze id&#39;s of CSS-klassen bevatten die beginnen met een cijfer, twee koppeltekens of een afbreekstreepje gevolgd door een cijfer (bijvoorbeeld #-123). (TNT-31061)
* Probleem verholpen dat werd geïntroduceerd met at.js 1.6.2, waarbij VEC-aanbiedingen (Visual Experience Composer) uit verschillende activiteiten die van toepassing zijn op dezelfde CSS-kiezer de prioriteit van de activiteit niet respecteerde. (TNT-31052)
* Probleem verholpen waarbij een belofte werd nagekomen in omgevingen waar geen native ondersteuning voor beloften bestond. (TNT-30974)
* Problemen worden nu correct vastgelegd en gerapporteerd via de gebeurtenis content-rendering mislukt. Eerder werd mogelijk gemeld dat JavaScript goed was uitgevoerd, zelfs als dat niet het geval was. (TNT-30599)

## at.js versie 1.6.2

Dit is een onderhoudsrelease en het volgende probleem wordt opgelost:

* Probleem verholpen waarbij sites van bepaalde klanten tot een oneindige &#39;async&#39;-lus leiden.

>[!WARNING]
>
>Daarnaast bevat at.js versie 1.6.2 ook alle verbeteringen en correcties die zijn opgenomen in at.js versie 1.6.1 en 1.6.0. Deze versies kunnen niet meer worden gedownload. Wij adviseren dat u aan versie 1.6.2 bevordert als het gebruiken van 1.6.1 of 1.6.0

Hier zijn de verhogingen en de moeilijke situaties die in at.js Versie 1.6.1 werden omvat:

* Probleem opgelost in at.js 1.6.0 dat ertoe leidde dat ervaringen met aanbevelingen werden gedupliceerd in Microsoft Internet Explorer 11. (TNT-30593)
* at.js zorgt er nu voor dat de logica voor het overschrijven van randen controleert of er een cookie met een randcluster bestaat om een ander randnummer te voorkomen als een gebruiker tijdens een sessie randen verlaat. (TNT-30563)
* Probleem verholpen waardoor at.js geen volgende handelingen kon uitvoeren als de HTML-inhoud ongeldige JS-code bevatte. at.js registreert nu de fout en geeft de resterende acties zonder kwestie terug. (TNT-30546)
* Er zijn wijzigingen aangebracht zodat er een uitzondering is wanneer een pagina omleiden wordt hergekwalificeerd voor een omleidingsactiviteit. (TNT-30532)
* Probleem verholpen waardoor de correcte time-out van de aanvraag niet kon worden doorgegeven aan de getOffer() API-aanvraag. (TNT-30498)
* Probleem verholpen waarbij het opslaan van cookies tijdens het gebruik van het bestandsprotocol door at.js 1.6.0 werd voorkomen. (TNT-30454)
* Het probleem dat ervoor zorgde dat niet alle ervaringen werden opgedaan met omleidingen tijdens het gebruik van [!DNL Analytics for Target] (A4T). (TNT-30444)
* Probleem verholpen waarbij de pagina werd verborgen achter de knop [!DNL Target] de vraag slaagt. (TNT-30358)

Hier zijn de verhogingen en de moeilijke situaties die in at.js Versie 1.6.0 werden omvat:

* Omleidingsvoorstellen worden nu automatisch ondersteund in de [!UICONTROL Analytics for Target] (A4T) integratie. De oplossing aan de clientzijde is verwijderd. (TNT-30247)
* Client-side edge routing is nu standaard ingeschakeld. (TNT-30261)
* Oplossing voor een probleem met VEC-actie (Visual Experience Composer) wanneer er afhankelijkheden zijn tussen handelingen. (TNT-30248)

## at.js Versie 1.5.0

at.js versie 1.5.0 is nu beschikbaar.

* De details van de `at-request-succeeded` -gebeurtenis bevat de omleidingsvlag. Met deze markering kunt u bepalen of de pagina wordt omgeleid naar een andere URL. Als u de URL wilt weten, meldt u zich aan `at-content-rendering-redirect`. (TNT-29834)
* Probleem verholpen dat ertoe heeft geleid `window.targetGlobalSettings.enabled` mislukt met een runtime-uitzondering als deze is ingesteld op false. (TNT-29829)
* Probleem verholpen die ertoe leidde dat de pagina mislukte tijdens het laden in Visual Experience Composer (VEC) als het gebruiken van douanecode aan een brand globale mbox verzoek en het gebruiken van lichaam het verbergen. (TNT-29795)
* Extra ondersteuning voor `screenOrientation`, `devicePixelRatio`, en `webGLRenderer`. Deze nieuwe [!DNL Target] aanvraagparameters worden gebruikt voor iPhone X en andere moderne apparaatdetectie. Zie voor meer informatie [Mobiel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html). (TNT-29781)
* Probleem verholpen waarbij de locatie-hint van de Adobe Audience Manager (AAM) niet altijd werd verzonden. (TNT-29695)
* Voor browsers die dit ondersteunen, schakelt at.js 1.5.0 over naar MutationObserver voor kiezersopiniepeiling. In versies vóór at.js 1.0.0 werd een MutationObserver-polyfill gebruikt, wat problematisch bleek te zijn. Om de polyfill problemen te voorkomen, gebruikt versie 1.5.0 de volgende pseudo-code om te bepalen welk planningsmechanisme moet worden gebruikt:

  ```
  if MutationObserver is supported
    scheduler = MutationObserver
  else if document is visible
    scheduler = requestAnimationFrame
  else
    scheduler = setTimeout
  ```

## at.js versie 1.3.0

at.js versie 1.3.0 is nu beschikbaar.

* De volgende nieuwe gebeurtenissen zijn beschikbaar om u te helpen bij het traceren, opsporen van fouten en het aanpassen van interactie met at.js:

   * LIBRARY_LOADED
   * REQUEST_START
   * CONTENT_RENDERING_START
   * CONTENT_RENDERING_NO_OFFERS
   * CONTENT_RENDERING_REDIRECT

  Zie voor meer informatie [at.js, aangepaste gebeurtenissen](/help/dev/implement/client-side/atjs/atjs-functions/atjs-custom-events.md).

* U kunt een verzoek at.js met extra parameters uitbreiden die uit gegevensleveranciers komen. Gegevensleveranciers moeten worden toegevoegd aan `window.targetGlobalSettings` onder de `dataProviders key`.

  Zie voor meer informatie [Gegevensleveranciers](atjs-functions/targetglobalsettings.md#data-providers).

* bij.js-aanvragen wordt nu GET gebruikt, maar er wordt overgeschakeld naar POST wanneer de URL groter is dan 2048 tekens. Er is een nieuwe eigenschap met de naam `urlSizeLimit` waar u de maximale grootte indien nodig kunt verhogen. Deze wijziging staat [!DNL Target] om at.js aan AppMeasurement uit te lijnen, dat de zelfde techniek gebruikt.
* [!DNL Target] nu de `mbox` in de `adobe.target.applyOffer(options)` functie wordt gebruikt. Deze sleutel is in het verleden vereist, maar [!DNL Target] handhaaft nu zijn gebruik om ervoor te zorgen dat [!DNL Target] heeft juiste validatie en klanten gebruiken de functie correct.
* at.js heeft de functie voor het bijhouden van gebeurtenissen verbeterd en klikt op tracking. at.js gebruikt `navigator.sendBeacon()` om gegevens voor het bijhouden van gebeurtenissen te verzenden en wordt teruggevallen naar synchrone XHR wanneer `navigator.sendBeacon()` wordt niet ondersteund. Deze fallback heeft vooral invloed op Internet Explorer 10 en 11 en op sommige versies van Safari. Safari voegt ondersteuning toe voor `navigator.sendBeacon()` in de komende iOS 11.3-release.
* Met at.js kunt u nu aanbiedingen renderen, zelfs als een pagina wordt geopend op tabbladen op de achtergrond. Sommige [!DNL Target] Klanten ondervonden een probleem toen `requestAnimationFrame()` is uitgeschakeld vanwege het browsergedrag voor achtergrondtabbladen.
* Deze versie voegt vele prestatiesverbeteringen, met inbegrip van kortere callstacks toe wanneer het inspecteren van een profiel van Chrome cpu.
* at.js 1.3.0 biedt geen ondersteuning meer voor de levering van inhoud in Microsoft Internet Explorer 9. Zie voor een lijst met ondersteunde browsers [Ondersteunde browsers](/help/dev/before-implement/supported-browsers.md). Alle aanvragen worden uitgevoerd via `XMLHttpRequest` met CORS-ondersteuning zonder JSONP-verzoeken. Deze wijziging verbetert de veiligheid aanzienlijk.

## at.js versie 1.2.3

at.js versie 1.2.3 is nu beschikbaar.

* Voegt ondersteuning toe voor JSON-aanbiedingen. JSON-aanbiedingen worden alleen ondersteund in activiteiten die zijn gemaakt met de Form-based Experience Composer. De enige manier om JSON-aanbiedingen te gebruiken is momenteel via directe API-aanroepen. Zie [JSON-aanbiedingen maken](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html).

## at.js versie 1.2.2

at.js versie 1.2.2 is nu beschikbaar.

* Probleem verholpen waarbij een JavaScript-fout werd geretourneerd bij het [!DNL Target] bibliotheek die op een pagina is geladen met de modus QUIRKS. (TNT-28312)
* Probleem verholpen dat ertoe heeft geleid [!DNL Target] klik op Tekstspatiëring om te breken [!DNL Analytics] de vraag van de gegevensinzameling. (TNT-28261)
* Probleem verholpen dat ertoe heeft geleid `getOffer() params` om te ontbreken wanneer `targetPageParams()` retourneert een lege tekenreeks. (TNT-28359)
* Probleem verholpen met genereren van sessie-id bij gebruik van alleen x. (TNT-28361)

## at.js versie 1.2.1

at.js versie 1.2.1 is nu beschikbaar.

* Probleem verholpen waarbij klikken op bijhouden op een koppeling met target=&quot;_blank&quot; voorkomen was [!DNL Target] vanaf het openen van de koppeling op een nieuw tabblad.

## at.js versie 1.2.0

at.js versie 1.2 is nu beschikbaar als onderhoudsversie die hoofdzakelijk insectenmoeilijke situaties bevat.

* Probleem verholpen waarbij standaardhandelingen voor speciale gevallen met muisklik werden voorkomen. (TNT-28089)
* Probleem verholpen waarbij klikken op bijhouden in een koppeling met `target="_blank"` dat [!DNL Target] vanaf het openen van de koppeling op een nieuw tabblad. (TNT-28072)
* IP de adressen kunnen als koekjesdomein worden gebruikt. (TNT-28002)
* Probleem verholpen dat flikkering veroorzaakte bij omleidingsvoorstellen met een global mbox of andere regionale dozen. (TNT-27978)
* Probleem opgelost in [!UICONTROL Experience Targeting] De opstelling van de activiteit ontbreekt binnen VEC wanneer het schakelen tussen Browse en stelt samen. (TNT-27942)
* Probleem verholpen met onjuiste afhandeling van flikkerstijlklassen voor kliktrackelementen. (TNT-27896)
* Probleem verholpen waarbij algemene mbox-parameters werden gemengd met alle mbox-parameters. (TNT-27846)
* Wijzigingen aangebracht om ervoor te zorgen dat Handlebars, Mustache en andere sjabloonbibliotheken aan de clientzijde correct worden afgehandeld door at.js. (TNT-27831)
* Wijzigingen aangebracht om ervoor te zorgen dat `sdidParamExpiry` wordt op de juiste wijze geïnitialiseerd en doorgegeven aan de Bezoeker-API. Deze regressie is toegevoegd aan `at.js 1.1.0`. De vorige versies at.js worden niet beïnvloed. Dit is alleen van invloed op clients die omleidingsaanbiedingen en A4T gebruiken. (TNT-27791)
* Wijzigingen aangebracht om ervoor te zorgen dat `SCRIPT` wordt uitgevoerd ongeacht het type-kenmerk dat wordt gebruikt. (TNT-27865)

## at.js versie 1.1.0

**Datum:** 2 augustus 2017

De volgende verbeteringen en correcties zijn opgenomen in at.js versie 1.1:

* Toegevoegde verwerking van responstoken. Zie voor meer informatie [Reactiepunten](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html).
* Het probleem is opgelost zodat `document.currentScript polyfill` interfereert niet met Angular 1.X.
* Wijzigingen aangebracht om ervoor te zorgen dat het bijhouden van klikken geen invloed heeft op de zichtbaarheidseigenschap. Klik op de volgende elementen worden gemarkeerd met de `at-element-click-tracking` CSS-klasse in plaats van `at-element-marker`.

## at.js Versie 1.0.0

**Datum:** 7 juli 2017

De volgende verbeteringen en correcties zijn opgenomen in versie 1.js 1.0:

* Ondersteuning voor asynchroon laden op .js voor sneller laden van pagina&#39;s.
* Ondersteuning voor het vooraf verbergen van pagina-inhoud bij het asynchroon laden van at.js.
* Betere foutberichten wanneer de levering van inhoud is uitgeschakeld.
* Prestatieverbeteringen bij het uitvoeren van meerdere activiteiten.
* Ondersteuning voor YUI-compressor.
* Foutenmelding voor aangepaste gebeurtenissen tijdens de levering van de activiteit.
* Oplossen voor prestatieproblemen in Microsoft Internet Explorer 11.
* Oplossen voor `getOffer()` functie die een fout geeft op sommige websites.
* Laad de [!DNL Target] bibliotheek asynchroon. Zie voor meer informatie [om.js Veelgestelde Vragen](/help/dev/implement/client-side/atjs/target-atjs-faq.md).

## at.js Versie 0.9.7

**Datum:** 22 mei 2017

De volgende verbeteringen en correcties zijn opgenomen in at.js versie 0.9.7:

* Probleem verholpen met betrekking tot een elementsleutel waarvan geen elementen aanwezig waren `insertAfter` en `insertBefore` handelingen in de Visual Experience Composer (VEC). Deze problemen hadden betrekking op de migratie van visuele aanbiedingen naar aanbiedingstemplates.

## at.js Versie 0.9.6

**Datum:** 13 april 2017

De volgende verbeteringen en correcties zijn opgenomen in at.js versie 0.9.6:

* Omleiding biedt ondersteuning voor A4T. Nadat u hebt gedownload en geïnstalleerd op versie 0.js 0.9.6, kunt u de omleidingsaanbiedingen gebruiken in activiteiten die [!UICONTROL Adobe Analytics as the Reporting Source for Target] (A4T). Naast at.js versie 0.9.6, zijn er andere minimumvereisten uw implementatie moet voldoen om te gebruiken doorleidt aanbiedingen en A4T. Voor meer informatie en extra belangrijke informatie zou u moeten weten, zie [Omleidingsvoorstellen - Veelgestelde vragen A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html).
* Vóór 0.js 0.9.6, toen de API voor bezoekers aanwezig was op de pagina en de `visitorApiTimeout` de instelling te agressief was, [!DNL Target] kan worden uitgevoerd in een situatie waarin er geen MCID-gegevens zijn verzonden in het dialoogvenster [!DNL Target] verzoek. Dit kan leiden tot problemen zoals onsite treffers in [!DNL Analytics] bij gebruik van A4T.

  Dit gedrag is gewijzigd in at.js 0.9.6, zelfs als `visitorApiTimeout` is ingesteld op 1 ms, [!DNL Target] zal proberen SDID, het volgen van servers, en de gegevens van klant IDs te verzamelen en die te verzenden in [!DNL Target] verzoek.

* De `selectorsPollingTimeout` instellen. Zie voor meer informatie [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).
* De indeling van de reactie van `getOffer()` is gewijzigd. Zie voor meer informatie [adobe.target.getOffer(opties)](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md).
* Logboekregistratie voor console is toegevoegd voor niet-ondersteunde toepassingen `<!DOCTYPE>` aangiften.
* Probleem verholpen waarbij [!DNL Target Classic] plug-ins werden niet correct toegepast wanneer meerdere standaardaanbiedingen naar één box werden verzonden. (TGT-22664)
* Verbeterde cookie-instelling voor twee TLD&#39;s (Top-Level-Domain) om ervoor te zorgen dat de box-cookie correct is ingesteld voor deze domeinen (bijvoorbeeld test.no, autodrives.ca, enzovoort).
* Het algoritme voor het extraheren van het domein op hoofdniveau dat moet worden gebruikt bij het opslaan van cookies is gewijzigd in versie 0.js 0.9.6. Vanwege deze wijziging kunnen cookies niet worden opgeslagen naar adressen die IP gebruiken. Meestal worden IP-adressen gebruikt voor testdoeleinden, maar als tijdelijke oplossingen kunt u DNS-vermeldingen gebruiken of het hostbestand op een lokaal vak aanpassen.
* Correctie van het verplaatsen en herschikken van handelingen waarbij eigenschappen tekenreekswaarden zijn in plaats van gehele getallen.

## at.js Versie 0.9.4

**Datum:** 19 januari 2017

* mbox-namen kunnen nu speciale tekens bevatten, waaronder ampersands ( &amp; ).

  Zie voor een lijst met toegestane speciale tekens [at.js-configuratie](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md).

* Toegevoegd `secureOnly` instelling die aangeeft of at.js alleen HTTPS mag gebruiken of mag schakelen tussen HTTP en HTTPS op basis van het paginaprotocol. Dit is een geavanceerde instelling die standaard op Onwaar wordt ingesteld en via `targetGlobalSettings`.
* De optie Verouderde browserondersteuning is beschikbaar in versie 0.js 0.9.3 en eerder. Deze optie is verwijderd in versie 0.js 0.9.4.

## at.js Versie 0.9.3

**Datum:** 10 oktober 2016

* Zorgt ervoor dat mbox in Microsoft Internet Explorer 11 vuur aanroept wanneer oudere browsers zijn uitgeschakeld in de instellingen at.js.
* Zorgt ervoor dat de standaardinhoud wordt teruggegeven als een dynamische verre aanbieding ontbreekt (bijvoorbeeld, als URL onjuist is en een fout 404 terugkeert).
* Zorgt ervoor dat elementen snel worden onthuld wanneer VEC klik-volgende selecteurs niet in DOM kan worden gevonden.

## at.js Versie 0.9.2

**Datum:** 21 september 2016

* Toegevoegde `optoutEnabled` instelling om de optie Weigeren apparaatgrafiek in of uit te schakelen. Als deze instelling is ingesteld op `true` en de bezoeker heeft ervoor gekozen het bijhouden te beëindigen , zal browser van de bezoeker geen mbox vraag maken. Apparaatgrafiek bevindt zich momenteel in bètaversie. Deze instelling is ingesteld op `false` standaard, maar moet worden ingesteld op `true` als u Apparaatgrafiek gebruikt.
* Toegevoegd `CustomEvent` steun voor het kennisgevingsmechanisme. Eerder kon het meldingsmechanisme voor de gebeurtenis at.js niet worden gebruikt via standaard DOM API&#39;s, zoals `document.addEventListener()`. Nu kunt u `document.addEventListener()` om in te schrijven op gebeurtenissen at.js, zoals aanvraaggebeurtenissen en content rendering gebeurtenissen.
* Oplossing voor een probleem met betrekking tot aanbiedingen die zijn gemaakt in Visual Experience Composer (VEC). Vóór deze release [!DNL Target] Verberg de kiezers en verberg deze alleen wanneer alle kiezers overeenkomen. In at.js 0.9.2 [!DNL Target] De kiezers worden uitgeschakeld zodra ze overeenkomen.

## at.js Versie 0.9.1

**Datum:** 14 juli 2016

* Verstrekt at.js een onderbreking voor de Dienst van identiteitskaart van de Bezoeker, die van de eigen onderbreking van de dienst onafhankelijk is.
* Hiermee wordt een probleem in 0.9.0 verholpen dat invloed had op implementaties met at.js op sommige pagina&#39;s en mbox.js (nu afgekeurd) op andere pagina&#39;s.
* Als u [!DNL Adobe Analytics] als rapportbron van uw activiteit, te hoeven u niet om een het volgen server tijdens activiteitenverwezenlijking te specificeren als u mbox.js versie 61 (of recenter) of versie 0.9.1 (of later) gebruikt. De bibliotheek at.js verzendt automatisch de waarden van de volgende server naar [!DNL Target]. Tijdens het creëren van activiteit, kunt u het het Volgen gebied van de Server op de Doelstellingen &amp; pagina van Montages leeg verlaten.

## at.js Versie 0.9.0

**[!DNL Target]Geen:** lid 6.1

**Datum:** 23 juni 2016

* Hiermee verhelpt u een whitescreen-probleem bij het gebruik van VEC-aanbiedingen. Iedereen die at.js gebruikt zou aan deze nieuwe versie moeten bevorderen.
* Nieuw `registerExtension` API.

  Deze nieuwe API biedt ontwikkelaars toegang tot bepaalde jQuery-modules die in at.js worden gebruikt om extensies (ook wel insteekmodules genoemd) voor de bibliotheek te ontwikkelen. Er zijn enkele gevolgen voor deze wijziging. Dit is alleen van invloed op gebruikers die de volgende functies gebruiken:

   * `getSettings()` API is verwijderd, maar dezelfde functionaliteit is beschikbaar via `registerExtension()`.
   * `getTracking()` API is verwijderd, maar dezelfde functionaliteit is beschikbaar via `registerExtension()`.

   * Bestaande extensies (bijvoorbeeld AngularJS-extensies) moeten worden bijgewerkt om de `registerExtension()` aanpak.

* Nieuwe API voor kennisgeving aan at.js.

  Het doel van dit kennisgevingssysteem is om meer inzicht te verschaffen in wat at.js doet op de pagina en wanneer er problemen zijn. Een veel voorkomend probleem met de VEC is dat een IT-release de pagina wijzigt, een VEC-kiezer afbreekt en de test stopt met het correct leveren van inhoud. Een doel van dit meldingssysteem is om deze leveringskwestie aan de pagina bekend te maken, zodat kunnen de ontwikkelaars tot deze informatie toegang hebben, het tot een systeem als [!DNL Adobe Analytics]en kan aan de bedrijfseigenaars worden gemeld dat hun test is mislukt.

* Nieuw `targetGlobalSettings()` API-methode.

  U kunt instellingen in de bibliotheek at.js overschrijven in plaats van ze te configureren in het dialoogvenster [!DNL Target Standard/Premium] UI of via REST API&#39;s.

## at.js Versie 0.8.0

**Datum:** 5 mei 2016.

Dit is de eerste officiële release van de bibliotheek at.js.

at.js is een nieuwe implementatiebibliotheek voor [!DNL Target] ontworpen voor zowel typische webimplementaties als toepassingen van één pagina.

at.js vervangt mbox.js voor [!DNL Adobe Target] implementaties.

Met at.js verbetert u onder andere de laadtijden van pagina&#39;s voor webimplementaties, verbetert u de beveiliging en biedt u betere implementatieopties voor toepassingen van één pagina.

at.js bevat de componenten die in target.js inbegrepen waren, zodat is er niet meer een vraag aan target.js.

Houd rekening met het volgende wanneer u at.js implementeert:

* Internet Explorer-versies ouder dan 8 worden niet ondersteund.
* Asynchrone implementatie betekent verouderde integratie zoals de [!UICONTROL Test&Target to SiteCatalyst] insteekmodule werkt mogelijk niet.
* [!DNL Target] plug-ins die verwijzen naar objecten en methoden mbox.js, worden niet ondersteund.
* Alle vraag aan [!DNL Target] worden gemaakt via XMLHTTPRequest en inhoud wordt geretourneerd via JSON.
