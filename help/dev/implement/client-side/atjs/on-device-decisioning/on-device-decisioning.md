---
keywords: implementatie, javascript bibliotheek, js, atjs, op apparatenbesluit, op apparatenbesluit, at.js, op apparaat, op apparaat, implementation0
description: Leer hoe u presteert [!UICONTROL on-device decisioning] met de bibliotheek at.js
title: Hoe werkt een apparaatbeslissing met de JavaScript-bibliotheek at.js?
feature: at.js
exl-id: bd0e062f-c259-46f3-adba-e380af058ac8
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '3531'
ht-degree: 1%

---

# [!UICONTROL On-device decisioning] for at.js

Vanaf versie 2.5.0 biedt at.js [!UICONTROL on-device decisioning]. [!UICONTROL On-device decisioning] laat u uw [A/B-test](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) en [Gericht op ervaring](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) activiteiten op browser om in geheugenbesluiten zonder een blokkerend netwerkverzoek aan browser uit te voeren [!DNL Adobe Target] Edge Network.

>[!NOTE]
>
>[!UICONTROL On-device decisioning] is beschikbaar voor zowel client-side als server-side implementaties. Dit artikel beschrijft [!UICONTROL on-device decisioning] voor client-side. Voor informatie over [!UICONTROL on-device decisioning] voor server-kant, verwijs naar de server-zijimplementatiedocumentatie [hier](../../../server-side/sdk-guides/on-device-decisioning/overview.md).

[!DNL Target] biedt ook de flexibiliteit om de meest relevante en meest recente ervaring van uw experimenteren en machine leergedreven (ML-gedreven) verpersoonlijkingsactiviteiten via een levende servervraag te leveren. Met andere woorden, wanneer prestaties het belangrijkst zijn, kunt u ervoor kiezen [!UICONTROL on-device decisioning]. Nochtans, wanneer de meest relevante, bijgewerkte, en ML-gedreven ervaring nodig is, kan een servervraag in plaats daarvan worden gemaakt.

## Wat zijn de voordelen van [!UICONTROL on-device decisioning]?

De voordelen van [!UICONTROL on-device decisioning] omvatten:

* **Kies voor supersnelle beslissingen en ervaringen.** De sluiting en de beslissing worden uitgevoerd in geheugen en op browser om het blokkeren van netwerkverzoeken te vermijden.
* **Verbeter de prestaties van de toepassing.** Voer experimenten uit en verpersoonlijking aan uw klanten en gebruikers zonder de ervaringen van de eindgebruiker in gevaar te brengen.
* **Kwaliteitsscore voor Google-site verbeteren.** Nu de beslissing in het geheugen plaatsvindt, verbetert u de score voor Google Site Quality van uw online bedrijf om deze beter zichtbaar te maken voor consumenten.
* **Leer van analyses in real time.** Krijg inzicht van uw activiteitsprestaties in real time via [Analyses voor doel](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) (A4T) rapportage. A4T staat u toe om uw strategie op kritieke momenten te draaien.

## Ondersteunde functies

De [!DNL Adobe Target] JS SDK biedt klanten de flexibiliteit om te kiezen tussen prestaties en versheid van gegevens voor beslissingen. Met andere woorden, als het voor u van het grootste belang is om de meest relevante en engaging van gepersonaliseerde inhoud via computerleren te leveren, moet er een live serveroproep worden gedaan. Maar als de prestaties kritischer zijn, moet een on-device en in-memory beslissing worden genomen. Voor [!UICONTROL on-device decisioning] Raadpleeg de lijst met ondersteunde functies voor meer informatie:

* Typen activiteiten
* Doelgerichtheid publiek
* Toewijzingsmethode

Zie voor meer informatie [Ondersteunde functies voor [!UICONTROL on-device decisioning]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md).

## Hoe werkt [!UICONTROL on-device decisioning] werken?

Wanneer u bij.js opstelt en initialiseert met [!UICONTROL on-device decisioning] enabled, a [regelartefact](/help/dev/implement/client-side/atjs/on-device-decisioning/rule-artifact.md) die uw [!UICONTROL on-device decisioning] voor A/B- en XT-activiteiten worden het publiek en de middelen gedownload van de dichtstbijzijnde Akamai CDN naar de bezoeker en lokaal in de browser van uw bezoeker in de cache geplaatst. Wanneer een verzoek van at.js wordt gedaan om een ervaring terug te winnen, wordt het besluit betreffende welke ervaring om in geheugen terug te keren wordt gemaakt, die op de meta-gegevens wordt gebaseerd in het caching regelartefact worden gecodeerd.

## Beslissingsmethode

Met [!UICONTROL on-device decisioning], [!DNL Target] introduceert een nieuwe instelling met de naam Decisioning Method. De instelling van de beslissingsmethode bepaalt hoe at.js uw ervaringen biedt. De beslissingsmethode heeft drie waarden:

* Alleen server
* Alleen op apparaat
* Hybride

### Alleen server

Server-kant slechts is de standaardbeslissingsmethode die uit de doos wordt geplaatst wanneer at.js 2.5.0+ wordt uitgevoerd en op uw Webeigenschappen opgesteld.

Het gebruiken van server-kant slechts als standaardconfiguratie betekent dat alle besluiten op [!DNL Target] edge network, wat een blokkerende servervraag impliceert. Deze aanpak kan incrementele vertraging introduceren, maar biedt ook aanzienlijke voordelen, zoals de mogelijkheid om deze toe te passen [!DNL Target]&#39;s machine-learningmogelijkheden die onder andere [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html), [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) (AP), en [Automatisch doel](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) activiteiten.

Bovendien kunt u uw persoonlijke ervaringen verbeteren door [!DNL Target]Het gebruikersprofiel van uw gebruiker, dat door zittingen en kanalen wordt voortgeduurd, kan krachtige resultaten voor uw zaken verstrekken.

Tot slot laat server-kant slechts u de Adobe Experience Cloud gebruiken en verfijnen publiek dat tegen door Audience Manager en de segmenten van Adobe Analytics kan worden gericht.

In het volgende diagram ziet u de interactie tussen uw bezoeker, de browser, at.js 2.5.0+ en de [!DNL Adobe Target] Edge-netwerk. In dit stroomdiagram worden nieuwe bezoekers en terugkerende bezoekers vastgelegd.

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![Stroomdiagram alleen op de server](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/server-side-only.png "Stroomdiagram alleen op de server"){zoomable="yes"}

De volgende lijst komt overeen met de cijfers in het diagram:

| Stap | Beschrijving |
| --- | --- |
| 1 | De Experience Cloud-bezoeker-id wordt opgehaald uit het dialoogvenster [Adobe Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?). |
| 2 | De bibliotheek at.js wordt synchroon geladen en de hoofdtekst van het document verborgen.<br />   De bibliotheek at.js kan ook asynchroon worden geladen met een optioneel vooraf verborgen fragment dat op de pagina is geïmplementeerd. |
| 3 | De bibliotheek at.js verbergt het lichaam om flikkering te voorkomen. |
| 4 | Er wordt een aanvraag voor het laden van een pagina ingediend die alle geconfigureerde parameters bevat, zoals (ECID, Customer ID, Custom Parameters, User Profile, enzovoort). |
| 5 | Profielscripts worden uitgevoerd en vervolgens toegevoegd aan de profielenwinkel.<br />In de profielopslag wordt een gekwalificeerd publiek aangevraagd vanuit de publieksbibliotheek (bijvoorbeeld een publiek dat wordt gedeeld vanuit Adobe Analytics, Adobe Audience Manager enzovoort).<br />Klantkenmerken worden in een batchproces naar de profielopslag verzonden. |
| 6 | De profielenopslag wordt gebruikt voor publiekskwalificatie en het opnemen aan filteractiviteiten. |
| 7 | De resulterende inhoud wordt geselecteerd nadat de ervaring via live is bepaald [!DNL Target] activiteiten. |
| 8 | De bibliotheek at.js verbergt de overeenkomstige elementen op de pagina die aan de ervaring worden geassocieerd die moet worden teruggegeven. |
| 9 | De bibliotheek at.js toont het lichaam zodat de rest van de pagina voor uw bezoeker aan mening kan worden geladen. |
| 10 | De bibliotheek at.js manipuleert DOM om de ervaring van uit te geven [!DNL Target] Edge Network. |
| 11 | De ervaring wordt weergegeven voor de bezoeker. |
| 12 | De hele webpagina wordt geladen. |
| 13 | De analysegegevens worden verzonden naar de servers van de Inzameling van Gegevens. |
| 14 | De gerichte gegevens worden aangepast aan de analysegegevens via SDID en worden verwerkt in de analytische rapporteringsopslag. De analysegegevens kunnen dan zowel in Analytics als [!DNL Target] via [!UICONTROL Analytics for Target] (A4T) verslagen. |

### Alleen op apparaat

Alleen op apparaat is de beslissingsmethode die moet worden ingesteld in at.js 2.5.0+ wanneer [!UICONTROL on-device decisioning] mag alleen op de volledige webpagina worden gebruikt.

[!UICONTROL On-device decisioning] kan uw ervaringen en verpersoonlijkingsactiviteiten bij het opblazen van snelle snelheid leveren omdat de beslissingen worden genomen op basis van een caching-artefact dat al uw activiteiten bevat die in aanmerking komen voor [!UICONTROL on-device decisioning].

Meer weten over welke activiteiten in aanmerking komen voor [!UICONTROL on-device decisioning], zie [Ondersteunde functies in [!UICONTROL on-device decisioning]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md).

Deze besluitvormingsmethode zou slechts moeten worden gebruikt als de prestaties hoogst kritiek over alle pagina&#39;s zijn die besluiten van Doel vereisen. Houd er bovendien rekening mee dat wanneer deze beslissingsmethode wordt geselecteerd, uw [!DNL Target] activiteiten die niet in aanmerking komen [!UICONTROL on-device decisioning] wordt niet geleverd of uitgevoerd. De bibliotheek at.js 2.5.0+ wordt gevormd om het caching regelartefact slechts te zoeken om besluiten te nemen.

In het volgende diagram ziet u de interactie tussen uw bezoeker, de browser, at.js 2.5.0+ en de CDN van Akamai. De Akamai CDN slaat het artefact van de regels voor het eerste bezoek van de bezoeker in het voorgeheugen op. Voor het eerste paginabezoek voor een nieuwe bezoeker, moet het artefact van de JSON- regels van Akamai CDN worden gedownload om plaatselijk op browser van de bezoeker in het voorgeheugen onder te brengen. Nadat het artefact van JSON-regels is gedownload, wordt de beslissing onmiddellijk genomen zonder een blokkerende netwerkaanroep. In het volgende stroomdiagram worden nieuwe bezoekers vastgelegd.

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![Stroomdiagram alleen op apparaat](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/on-device-only.png "Stroomdiagram alleen op apparaat"){zoomable="yes"}

De volgende lijst komt overeen met de cijfers in het diagram:

>[!NOTE]
>
>[!DNL Adobe Target] Beheerdersservers kwalificeren al uw activiteiten waarvoor [!UICONTROL on-device decisioning], genereert u het artefact van de JSON-regels en geeft u dit door aan de Akamai CDN. Uw activiteiten worden voortdurend gecontroleerd op updates om een nieuw Artefact van JSON-regels uit te voeren dat aan Akamai CDN moet worden doorgegeven.

| Stap | Beschrijving |
| --- | --- |
| 1 | De Experience Cloud-bezoeker-id wordt opgehaald uit het dialoogvenster [Adobe Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | De bibliotheek at.js wordt synchroon geladen en de hoofdtekst van het document verborgen.<br />De bibliotheek at.js kan ook asynchroon worden geladen met een optioneel vooraf verborgen fragment dat op de pagina is geïmplementeerd. |
| 3 | De bibliotheek at.js verbergt het lichaam om flikkering te voorkomen. |
| 4 | De bibliotheek at.js vraagt om het JSON-regelartefact van de dichtstbijzijnde Akamai CDN naar de bezoeker op te halen. |
| 5 | De Akamai CDN reageert met het Artefact van de JSON-regel. |
| 6 | De JSON-regelartefact wordt lokaal in de browser van de bezoeker in cache geplaatst. |
| 7 | De bibliotheek at.js interpreteert het JSON-regelartefact en voert het besluit uit om de ervaring op te halen en verbergt de geteste elementen. |
| 8 | De bibliotheek at.js toont het lichaam zodat de rest van de pagina voor uw bezoeker aan mening kan worden geladen. |
| 9 | De bibliotheek at.js manipuleert DOM om de ervaring van het caching JSON regelartefact terug te geven. |
| 10 | De ervaring wordt weergegeven voor de bezoeker. |
| 11 | De hele webpagina wordt geladen. |
| 12 | De analysegegevens worden verzonden naar de servers van de Inzameling van Gegevens. De gerichte gegevens worden aangepast aan de analysegegevens via SDID en worden verwerkt in de analytische rapporteringsopslag. De analysegegevens kunnen dan zowel in Analytics als [!DNL Target] via [!UICONTROL Analytics for Target] (A4T) verslagen. |

In het volgende diagram ziet u de interactie tussen uw bezoeker, de browser, op .js 2.5.0+ en de JSON-regelartefact in de cache voor het volgende paginahit of terugkerend bezoek van de bezoeker. Omdat het artefact van JSON-regels al in het cachegeheugen is opgeslagen en beschikbaar is in de browser, wordt de beslissing onmiddellijk genomen zonder een blokkerende netwerkaanroep. Dit stroomdiagram legt volgende paginanavigatie of terugkerende bezoekers vast.

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![Stroomdiagram alleen op apparaat voor paginanavigatie en herhaalde bezoeken](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/on-device-only-subsequent.png "Stroomdiagram alleen op apparaat voor paginanavigatie en herhaalde bezoeken"){zoomable="yes"}

De volgende lijst komt overeen met de cijfers in het diagram:

>[!NOTE]
>
>[!DNL Adobe Target] Beheerdersservers kwalificeren al uw activiteiten waarvoor [!UICONTROL on-device decisioning], genereert u het artefact van de JSON-regels en geeft u dit door aan de Akamai CDN. Uw activiteiten worden voortdurend gecontroleerd op updates om een nieuw Artefact van JSON-regels uit te voeren dat aan Akamai CDN moet worden doorgegeven.

| Stap | Beschrijving |
| --- | --- |
| 1 | De Experience Cloud-bezoeker-id wordt opgehaald uit het dialoogvenster [Adobe Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | De bibliotheek at.js wordt synchroon geladen en de hoofdtekst van het document verborgen.<br />De bibliotheek at.js kan ook asynchroon worden geladen met een optioneel vooraf verborgen fragment dat op de pagina is geïmplementeerd. |
| 3 | De bibliotheek at.js verbergt het lichaam om flikkering te voorkomen. |
| 4 | De bibliotheek at.js interpreteert het JSON-regelartefact en voert de beslissing in het geheugen uit om de ervaring op te halen. |
| 5 | De geteste elementen zijn verborgen. |
| 6 | De bibliotheek at.js toont het lichaam zodat de rest van de pagina voor uw bezoeker aan mening kan worden geladen. |
| 7 | De bibliotheek at.js manipuleert DOM om de ervaring van het caching JSON regelartefact terug te geven. |
| 8 | De ervaring wordt weergegeven voor de bezoeker. |
| 9 | De hele webpagina wordt geladen. |
| 10 | De analysegegevens worden verzonden naar de servers van de Inzameling van Gegevens. De gerichte gegevens worden aangepast aan de analysegegevens via SDID en worden verwerkt in de analytische rapporteringsopslag. De analysegegevens kunnen dan zowel in Analytics als [!DNL Target] via [!UICONTROL Analytics for Target] (A4T) verslagen. |

### Hybride

Hybride is de beslissingsmethode die in at.js 2.5.0+ moet worden geplaatst wanneer allebei [!UICONTROL on-device decisioning] en activiteiten die een netwerkaanroep van de [!DNL Adobe Target] Edge-netwerk moet worden uitgevoerd.

Wanneer u beide beheert [!UICONTROL on-device decisioning] activiteiten en serveractiviteiten, kan het een beetje gecompliceerd en vervelend zijn wanneer het denken over hoe te om en levering op te stellen [!DNL Target] op uw pagina&#39;s. met hybride als beslissingsmethode, [!DNL Target] weet wanneer het een servervraag aan moet maken [!DNL Adobe Target] Het netwerk van de rand voor activiteiten die server-zijuitvoering vereisen, en ook wanneer om slechts op-apparatenbesluiten uit te voeren.

Het Artefact van de JSON-regels bevat metagegevens om at.js te laten weten of een box een serveractiviteit heeft die wordt uitgevoerd of een [!UICONTROL on-device decisioning] activiteit. Deze beslissingsmethode zorgt ervoor dat activiteiten die u snel wilt uitvoeren, worden uitgevoerd [!UICONTROL on-device decisioning] en voor activiteiten die krachtigere ML-gedreven verpersoonlijking vereisen, worden die activiteiten gedaan via [!DNL Adobe Target] Edge-netwerk.

In het volgende diagram ziet u de interactie tussen uw bezoeker, de browser, at.js 2.5.0+, de Akamai CDN en de [!DNL Adobe Target] Edge Network (Edge Network) voor een nieuwe bezoeker die uw pagina voor het eerst bezoekt. De afstand van dit diagram is dat het artefact van de JSON-regels asynchroon wordt gedownload terwijl de beslissingen via het [!DNL Adobe Target] Edge-netwerk.

Deze benadering zorgt ervoor dat de grootte van het artefact, dat vele activiteiten kan omvatten, niet negatief de latentie van de beslissing beïnvloedt. Het synchroon downloaden van de JSON-regels en het vervolgens nemen van de beslissing kan ook negatieve gevolgen hebben voor de latentie en kan inconsistent zijn. Daarom is de hybride besluitvormingsmethode een beste praktijkaanbeveling om altijd een server-zijvraag voor het besluit voor een nieuwe bezoeker te maken, en aangezien de JSON regels artefact parallel in het voorgeheugen wordt opgeslagen. Voor om het even welke verdere paginabezoeken en terugkeerbezoeken, worden de besluiten genomen van het geheime voorgeheugen en in geheugen door het JSON regelartefact.

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![Hybride-stroomdiagram voor een eerste bezoeker](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/hybrid-first-time-visitor.png "Hybride-stroomdiagram voor een eerste bezoeker"){zoomable="yes"}

De volgende lijst komt overeen met de cijfers in het diagram:

>[!NOTE]
>
>[!DNL Adobe Target] Beheerdersservers kwalificeren al uw activiteiten waarvoor [!UICONTROL on-device decisioning], genereert u het artefact van de JSON-regels en geeft u dit door aan de Akamai CDN. Uw activiteiten worden voortdurend gecontroleerd op updates om een nieuw Artefact van JSON-regels uit te voeren dat aan Akamai CDN moet worden doorgegeven.

| Stap | Beschrijving |
| --- | --- |
| 1 | De Experience Cloud-bezoeker-id wordt opgehaald uit het dialoogvenster [Adobe Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | De bibliotheek at.js wordt synchroon geladen en de hoofdtekst van het document verborgen.<br />De bibliotheek at.js kan ook asynchroon worden geladen met een optioneel vooraf verborgen fragment dat op de pagina is geïmplementeerd. |
| 3 | De bibliotheek at.js verbergt het lichaam om flikkering te voorkomen. |
| 4 | Er wordt een aanvraag voor het laden van pagina&#39;s ingediend bij de [!DNL Adobe Target] Edge Network, inclusief alle geconfigureerde parameters zoals (ECID, Customer ID, Custom Parameters, User Profile, enzovoort). |
| 5 | Parallel hieraan vraagt at.js om het Artefact van de JSON-regel van de dichtstbijzijnde Akamai CDN naar de bezoeker op te halen. |
| 6 | ([!DNL Adobe Target] Edge Network)-profielscripts worden uitgevoerd en vervolgens toegevoegd aan de profielopslag. In de profielopslag wordt een gekwalificeerd publiek aangevraagd vanuit de publieksbibliotheek (bijvoorbeeld een publiek dat wordt gedeeld vanuit Adobe Analytics, Adobe Audience Manager enzovoort). |
| 7 | De Akamai CDN reageert met het Artefact van de JSON-regel. |
| 8 | De profielenopslag wordt gebruikt voor publiekskwalificatie en het opnemen aan filteractiviteiten. |
| 9 | De resulterende inhoud wordt geselecteerd nadat de ervaring via live is bepaald [!DNL Target] activiteiten. |
| 10 | De bibliotheek at.js verbergt de overeenkomstige elementen op de pagina die aan de ervaring worden geassocieerd die moet worden teruggegeven. |
| 11 | De bibliotheek at.js toont het lichaam zodat de rest van de pagina voor uw bezoeker aan mening kan worden geladen. |
| 12 | De bibliotheek at.js manipuleert DOM om de ervaring van uit te geven [!DNL Target] Edge Network. |
| 13 | De ervaring wordt weergegeven voor de bezoeker. |
| 14 | De hele webpagina wordt geladen. |
| 15 | De analysegegevens worden verzonden naar de servers van de Inzameling van Gegevens. De gerichte gegevens worden aangepast aan de analysegegevens via SDID en worden verwerkt in de analytische rapporteringsopslag. De analysegegevens kunnen dan zowel in Analytics als [!DNL Target] via [!UICONTROL Analytics for Target] (A4T) verslagen. |

Het volgende diagram illustreert de interactie tussen uw bezoeker, browser, at.js 2.5.0+, en het caching JSON regelt artefact voor een verdere paginanavigatie of een terugkeerbezoek. In dit diagram, concentreert zich slechts op het gebruiksgeval dat een op-apparatenbesluit voor de verdere paginanavigatie of terugkeerbezoek wordt genomen. Houd in mening dat afhankelijk van welke activiteiten voor bepaalde pagina&#39;s levend zijn, een server-zijvraag kan worden gemaakt om server-zijbesluiten uit te voeren.

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![Hybride-stroomdiagram voor paginanavigatie en herhaalde bezoeken](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/hybrid-subsequent.png "Hybride-stroomdiagram voor paginanavigatie en herhaalde bezoeken"){zoomable="yes"}

De volgende lijst komt overeen met de cijfers in het diagram:

>[!NOTE]
>
>[!DNL Adobe Target] Beheerdersservers kwalificeren al uw activiteiten waarvoor [!UICONTROL on-device decisioning], genereert u het artefact van de JSON-regels en geeft u dit door aan de Akamai CDN. Uw activiteiten worden voortdurend gecontroleerd op updates om een nieuw Artefact van JSON-regels uit te voeren dat aan Akamai CDN moet worden doorgegeven.

| Stap | Beschrijving |
| --- | --- |
| 1 | De Experience Cloud-bezoeker-id wordt opgehaald uit het dialoogvenster [Adobe Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | De bibliotheek at.js wordt synchroon geladen en de hoofdtekst van het document verborgen.<br />De bibliotheek at.js kan ook asynchroon worden geladen met een optioneel vooraf verborgen fragment dat op de pagina is geïmplementeerd. |
| 3 | De bibliotheek at.js verbergt het lichaam om flikkering te voorkomen. |
| 4 | Er wordt een verzoek ingediend om een ervaring op te halen. |
| 5 | De bibliotheek at.js bevestigt dat het JSON-regelartefact al in de cache is geplaatst en voert het besluit in het geheugen uit om de ervaring op te halen. |
| 6 | De geteste elementen zijn verborgen. |
| 7 | De bibliotheek at.js toont het lichaam zodat de rest van de pagina voor uw bezoeker aan mening kan worden geladen. |
| 8 | De bibliotheek at.js manipuleert DOM om de ervaring van het caching JSON regelartefact terug te geven. |
| 9 | De ervaring wordt weergegeven voor de bezoeker. |
| 10 | De hele webpagina wordt geladen. |
| 11 | De analysegegevens worden verzonden naar de servers van de Inzameling van Gegevens. De gerichte gegevens worden aangepast aan de analysegegevens via SDID en worden verwerkt in de analytische rapporteringsopslag. De analysegegevens kunnen dan zowel in Analytics als [!DNL Target] via [!UICONTROL Analytics for Target] (A4T) verslagen. |

## Hoe kan ik [!UICONTROL on-device decisioning]?

[!UICONTROL On-device decisioning] is beschikbaar voor iedereen [!DNL Target] klanten die At.js 2.5.0+ gebruiken.

Inschakelen [!UICONTROL on-device decisioning]:

>[!NOTE]
>
>U moet de beheerder of fiatteur hebben [gebruikersrol](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) om de beslissingstoegang op het apparaat in of uit te schakelen.

1. Klik op **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]**.
1. Onder **[!UICONTROL Account details]**, schuiven de **[!UICONTROL On-Device Decisioning]** schakelen naar de positie &quot;aan&quot;.

   ![[!UICONTROL On-device decisioning] schakelen](assets/on-device-decisioning-toggle.png)

   &quot;Alle bestaande [!UICONTROL on-device decisioning] de optie &#39;gekwalificeerde activiteiten&#39; wordt weergegeven als u [!UICONTROL on-device decisioning].
1. (Voorwaardelijk) Schuif de schakeloptie naar de positie &quot;Aan&quot; als u al uw actieve elementen wilt [!DNL Target] activiteiten waarvoor [!UICONTROL on-device decisioning] automatisch in het artefact worden opgenomen.

   Als u deze schakeloptie uitschakelt, moet u alle [!UICONTROL on-device decisioning] activiteiten die erop gericht zijn deze op te nemen in de gegenereerde artefact. Met andere woorden, elke activiteit in live-toestand voordat de beslissingsschakeloptie op het apparaat wordt ingeschakeld, is niet opgenomen in het artefact van de regels.

Na het inschakelen van de beslissingsschakelaar op het apparaat, [!DNL Target] begint het produceren en het verspreiden [regelartefacten](/help/dev/implement/client-side/atjs/on-device-decisioning/rule-artifact.md) voor uw client.

>[!WARNING]
>
>Zorg ervoor dat u de schakeloptie inschakelt voordat u de [!DNL Adobe Target] SDK voor gebruik [!UICONTROL on-device decisioning]. De regelartefacten moeten eerst aan Akamai CDNs produceren en verspreiden voor [!UICONTROL on-device decisioning] om te werken. De propagatie kan vijf tot tien minuten voor het eerste regelartefact vergen om aan Akamai CDN te produceren en te verspreiden.

## Hoe kan ik bij .js 2.5.0+ te gebruiken configureren [!UICONTROL on-device decisioning]?

1. Klik op **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]**.
1. Onder **[!UICONTROL Implementation Methods]** > **[!UICONTROL Main Implementation Method]**, klikt u op **[!UICONTROL Edit]** naast uw versie at.js (moet zich bevinden op .js 2.5.0 of hoger).

   ![Instellingen van hoofdimplementatiemethode bewerken](assets/main-implementation-method.png)

   >[!WARNING]
   >
   >Voordat u deze standaardinstellingen wijzigt, raadpleegt u eerst de Client Care om te voorkomen dat de huidige implementatie wordt beïnvloed.

1. Selecteer de gewenste beslissingsmethode:

   * Alleen server
   * Alleen op apparaat
   * Hybride

   ![Bewerken bij.js, instellingenvenster](assets/global-settings.png)

### Algemene instellingen

U kunt een standaardbeslissingsmethode configureren voor alle [!DNL Target] besluiten. De verschillende besluitvormingsmethodes zijn server-kant slechts, slechts op apparaat, en Hybrid. De beslissingsmethode die is geselecteerd in het dialoogvenster [!DNL Target] UI is geconfigureerd in `window.targetGlobalSettings` onder de `decisioningMethod` veld. Meer informatie over de `decisioningMethod` in [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#decisioningmethod).

```javascript {line-numbers="true"}
<head> 
    <script type="text/javascript">

        window.targetGlobalSettings = { 
            clientCode: "yourClientCodeHere", 
            imsOrgId: "imsOrgId@AdobeOrg", 
            decisioningMethod: "on-device"

        }; 
    </script>

    <script type="text/javascript" src="at.js"></script> 
</head>
```

### Aangepaste instelling

Als u de `decisioningMethod` in `window.targetGlobalSettings`, maar wil de `decisioningMethod` voor elke [!DNL Adobe Target] beslissing volgens uw gebruikscase, kunt u deze procedure doen door te specificeren `decisioningMethod` in At.js2.5.0+&#39;s [getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) vraag.

```javascript {line-numbers="true"}
adobe.target.getOffers({ 

  decisioningMethod:"on-device", 
  request: { 
    execute: { 
      mboxes: [ 
        { 
          index: 0, 
          name: "homepage" 
        } 
      ] 
    } 
 } 
});
```

>[!NOTE]
>
>Als u &quot;op apparaat&quot; of &quot;hybride&quot; wilt gebruiken als een beslissingsmethode in de aanroep getOffers(), moet u ervoor zorgen dat de algemene instelling `decisioningMethod` als &quot;op apparaat&quot; of &quot;hybride&quot;. De bibliotheek at.js 2.5.0+ moet weten of om het Artefact van de regels JSON onmiddellijk na het laden op de pagina te downloaden en in het voorgeheugen onder te brengen. Als de besluitvormingsmethode voor het globale plaatsen aan &quot;server-kant&quot;wordt geplaatst, en &quot;op-apparaat&quot;of &quot;hybride&quot;besluitvormingsmethode wordt overgegaan in de getOffers () vraag, zou at.js 2.5.0+ niet het JSON regelartefact in het voorgeheugen ondergebracht hebben om uw op-apparatenbesluiten uit te voeren.

### Artefactcache TTL

Het doel vertegenwoordigt uw activiteiten waarvoor [!UICONTROL on-device decisioning] als een artefact dat uit meta-gegevens, regels, en voorwaarden bestaat. Dit artefact wordt in het cachegeheugen opgeslagen op de Akamai CDN. Tijdens het eerste bezoek van uw gebruiker, downloadt browser van de gebruiker en caches het artefact dat uw [!UICONTROL on-device decisioning] activiteiten.

Bij volgende bezoeken aan uw site controleert de browser automatisch of er een nieuwere versie van het artefact moet worden gedownload. Met deze controle wordt latentie toegevoegd. De Artefacache TTL definieert het aantal minuten dat de browser niet mag controleren op een bijgewerkt artefact sinds de laatste geslaagde download. Hoe langer het tijdsbestek, hoe beter de prestaties. Hoe korter het tijdkader, hoe beter de gegevens worden versnipperd, maar dit gaat ten koste van extra latentie.

## Hoe weet ik dat een activiteit [!UICONTROL on-device decisioning] subsidiabel?

Nadat u een activiteit creeert die [!UICONTROL on-device decisioning] in aanmerking komend, een etiket dat Beslissingen op Apparaat Geschikt leest, is zichtbaar in de pagina van het Overzicht van de activiteit.

![Op Apparaatbeslissingslabel komt in aanmerking voor de pagina Overzicht van de activiteit.](assets/on-device-decisioning-eligible-label.png)

Dit label betekent niet dat de activiteit altijd via [!UICONTROL on-device decisioning]. Alleen wanneer at.js 2.5.0+ is geconfigureerd voor gebruik [!UICONTROL on-device decisioning] zal deze activiteit op apparaat worden uitgevoerd. Als at.js 2.5.0+ niet wordt gevormd om op-apparaat te gebruiken, dan zal deze activiteit nog via een servervraag worden geleverd die van at.js wordt gemaakt.

U kunt filteren op alle activiteiten die [!UICONTROL on-device decisioning] komt in aanmerking op de pagina Activiteiten via het filter In aanmerking komende beslissing op apparaat.

![In aanmerking komend filter voor apparaatbesluitvorming op de pagina Activiteiten.](assets/on-device-decisioning-filter.png)

>[!NOTE]
>
>Na het maken en activeren van een activiteit die [!UICONTROL on-device decisioning] In aanmerking komend, kan het vijf tot tien minuten nemen alvorens het in het regelvervorming inbegrepen is die aan het punt van aanwezigheid Akamai CDN wordt geproduceerd en verspreid.

## Overzicht van stappen om mijn [!UICONTROL on-device decisioning] activiteiten worden geleverd via At.js 2.5.0+?

1. Toegang krijgen tot de [!DNL Adobe Target] UI en navigeer naar **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account Details]** de **[!UICONTROL On-Device Decisioning]** schakelen.
1. De optie **[!UICONTROL "Include all existing [!UICONTROL on-device decisioning] qualified activities in the artifact"]** schakelen.

   De eerste JSON-regels kunnen tot 10 minuten duren.

1. Een [Type activiteit dat door wordt gesteund [!UICONTROL on-device decisioning]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md)en gaat na of [!UICONTROL on-device decisioning] subsidiabel.
1. Stel de **[!UICONTROL Decisioning Method]** hetzij **[!UICONTROL "Hybrid"]** of **[!UICONTROL "On-device only"]** via de interface voor instellingen bij.js.
1. Download en implementeer At.js 2.5.0+ op uw pagina&#39;s.
