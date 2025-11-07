---
keywords: implementatie, javascript bibliotheek, js, atjs, op apparatenbesluit, op apparatenbesluit, at.js, op apparaat, op apparaat, implementation0
description: Leer hoe u [!UICONTROL on-device decisioning] kunt uitvoeren met de bibliotheek at.js
title: Hoe werkt een apparaatbeslissing met de JavaScript-bibliotheek at.js?
feature: at.js
exl-id: bd0e062f-c259-46f3-adba-e380af058ac8
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '3478'
ht-degree: 1%

---

# [!UICONTROL On-device decisioning] for at.js

Vanaf versie 2.5.0 biedt at.js [!UICONTROL on-device decisioning] aan. [!UICONTROL On-device decisioning] laat u uw [&#x200B; Test A/B &#x200B;](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=nl-NL) in het voorgeheugen onderbrengen en [&#x200B; Ervaring richtend &#x200B;](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html?lang=nl-NL) (XT) activiteiten op browser om in-geheugenbesluiten zonder een blokkerend netwerkverzoek aan [!DNL Adobe Target] Edge Network uit te voeren.

>[!NOTE]
>
>[!UICONTROL On-device decisioning] is beschikbaar voor zowel client-side als server-side implementaties. In dit artikel wordt [!UICONTROL on-device decisioning] beschreven voor client-side. Voor informatie betreffende [!UICONTROL on-device decisioning] voor server-kant, verwijs hier de server-zijimplementatiedocumentatie [&#x200B; &#x200B;](../../../server-side/sdk-guides/on-device-decisioning/overview.md).

[!DNL Target] biedt ook de flexibiliteit om de meest relevante en meest recente ervaring van uw experimenteren en machine leergedreven (ML-gedreven) verpersoonlijkingsactiviteiten via een levende servervraag te leveren. Met andere woorden, wanneer prestaties het belangrijkst zijn, kunt u ervoor kiezen om [!UICONTROL on-device decisioning] te gebruiken. Nochtans, wanneer de meest relevante, bijgewerkte, en ML-gedreven ervaring nodig is, kan een servervraag in plaats daarvan worden gemaakt.

## Wat zijn de voordelen van [!UICONTROL on-device decisioning]?

De voordelen van [!UICONTROL on-device decisioning] zijn onder andere:

* **lever het opblazen snelle besluiten en ervaringen.** De sluiting en de beslissing worden uitgevoerd in het geheugen en op browser om het blokkeren van netwerkverzoeken te vermijden.
* **verbeter toepassingsprestaties.** Voer experimenten uit en lever personalisatie aan uw klanten en gebruikers zonder de ervaringen van eindgebruikers in gevaar te brengen.
* **verbeter de Score van de Kwaliteit van de Plaats van Google.** Nu de beslissing in het geheugen plaatsvindt, verbetert u de score voor kwaliteit van de Google-site van uw onlinebedrijf om deze beter door de consument te kunnen ontdekken.
* **leer van analyses in real time.** de Inzichten van de winst van uw activiteitenprestaties in real time via [&#x200B; Analytics voor Doel &#x200B;](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=nl-NL) (A4T) rapporterend. A4T staat u toe om uw strategie op kritieke momenten te draaien.

## Ondersteunde functies

De [!DNL Adobe Target] JS SDK biedt klanten de flexibiliteit om te kiezen tussen prestaties en versheid van gegevens voor beslissingen. Met andere woorden, als het voor u van het grootste belang is om de meest relevante en engaging van gepersonaliseerde inhoud via computerleren te leveren, moet er een live serveroproep worden gedaan. Maar als de prestaties kritischer zijn, moet een on-device en in-memory beslissing worden genomen. [!UICONTROL on-device decisioning] werkt alleen als u de lijst met ondersteunde functies bekijkt:

* Typen activiteiten
* Doelgerichtheid publiek
* Toewijzingsmethode

Voor meer informatie, zie [&#x200B; Gesteunde eigenschappen voor [!UICONTROL on-device decisioning]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md).

## Hoe werkt [!UICONTROL on-device decisioning]?

Wanneer u bij.js met [!UICONTROL on-device decisioning] toegelaten opstelt en initialiseert, a [&#x200B; regelartefact &#x200B;](/help/dev/implement/client-side/atjs/on-device-decisioning/rule-artifact.md) dat uw [!UICONTROL on-device decisioning] voor A/B en XT activiteiten, publiek, en activa omvat, wordt gedownload van dichtste Akamai CDN aan uw bezoeker en plaatselijk in het voorgeheugen ondergebracht op browser van uw bezoeker. Wanneer een verzoek van at.js wordt gedaan om een ervaring terug te winnen, wordt het besluit betreffende welke ervaring om in geheugen terug te keren wordt gemaakt, die op de meta-gegevens wordt gebaseerd in het caching regelartefact worden gecodeerd.

## Beslissingsmethode

Met [!UICONTROL on-device decisioning] introduceert [!DNL Target] een nieuwe instelling met de naam Decisioning Method. De instelling van de beslissingsmethode bepaalt hoe at.js uw ervaringen biedt. De beslissingsmethode heeft drie waarden:

* Alleen server
* Alleen op apparaat
* Hybride

### Alleen server

Server-kant slechts is de standaardbeslissingsmethode die uit de doos wordt geplaatst wanneer at.js 2.5.0+ wordt uitgevoerd en op uw Webeigenschappen opgesteld.

Als alleen server-side wordt gebruikt als de standaardconfiguratie, worden alle beslissingen genomen in het [!DNL Target] edge-netwerk. Dit houdt in dat de server wordt geblokkeerd. Deze benadering kan stijgende latentie introduceren, maar het verstrekt ook significante voordelen, zoals het geven van u de capaciteit om [!DNL Target] machine-leert mogelijkheden van toepassing te zijn die [&#x200B; Aanbevelingen &#x200B;](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html?lang=nl-NL) omvatten, [&#x200B; Automated Personalization &#x200B;](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html?lang=nl-NL) (AP), en [&#x200B; auto-Doel &#x200B;](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html?lang=nl-NL) activiteiten.

Bovendien kan het verbeteren van uw persoonlijke ervaringen door het gebruikersprofiel van [!DNL Target] te gebruiken, dat door sessies en kanalen blijft bestaan, krachtige resultaten voor uw bedrijf opleveren.

Ten slotte kunt u met de server alleen de Adobe Experience Cloud gebruiken en het publiek afstemmen waarvoor u een doelgericht beroep kunt doen via de segmenten Audience Manager en Adobe Analytics.

In het volgende diagram ziet u de interactie tussen uw bezoeker, de browser, at.js 2.5.0+ en het [!DNL Adobe Target] Edge-netwerk. In dit stroomdiagram worden nieuwe bezoekers en terugkerende bezoekers vastgelegd.

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![&#x200B; server-zij slechts stroomdiagram &#x200B;](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/server-side-only.png " server-zij slechts stroomdiagram "){zoomable="yes"}

De volgende lijst komt overeen met de cijfers in het diagram:

| Stap | Beschrijving |
| --- | --- |
| 1 | De identiteitskaart van de Bezoeker van Experience Cloud wordt teruggewonnen van de [&#x200B; Dienst van de Identiteit van Adobe Experience Cloud &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=nl-NL&). |
| 2 | De bibliotheek at.js wordt synchroon geladen en de hoofdtekst van het document verborgen.<br />   De bibliotheek at.js kan ook asynchroon worden geladen met een optioneel vooraf verborgen fragment dat op de pagina is geïmplementeerd. |
| 3 | De bibliotheek at.js verbergt het lichaam om flikkering te voorkomen. |
| 4 | Er wordt een aanvraag voor het laden van een pagina ingediend die alle geconfigureerde parameters bevat, zoals (ECID, Customer ID, Custom Parameters, User Profile, enzovoort). |
| 5 | Profielscripts worden uitgevoerd en vervolgens toegevoegd aan de profielenwinkel.<br /> de Opslag van het Profiel vraagt gekwalificeerd publiek van de Bibliotheek van het Publiek (bijvoorbeeld, publiek dat van Adobe Analytics, Adobe Audience Manager wordt gedeeld, etc.).<br /> de attributen van de Klant worden verzonden naar de Opslag van het Profiel in een partijproces. |
| 6 | De profielenopslag wordt gebruikt voor publiekskwalificatie en het opnemen aan filteractiviteiten. |
| 7 | De resulterende inhoud wordt geselecteerd nadat de ervaring is bepaald op basis van live [!DNL Target] -activiteiten. |
| 8 | De bibliotheek at.js verbergt de overeenkomstige elementen op de pagina die aan de ervaring worden geassocieerd die moet worden teruggegeven. |
| 9 | De bibliotheek at.js toont het lichaam zodat de rest van de pagina voor uw bezoeker aan mening kan worden geladen. |
| 10 | De bibliotheek at.js manipuleert de DOM om de ervaring van [!DNL Target] Edge Network terug te geven. |
| 11 | De ervaring wordt weergegeven voor de bezoeker. |
| 12 | De hele webpagina wordt geladen. |
| 13 | De analysegegevens worden verzonden naar de servers van de Inzameling van Gegevens. |
| 14 | De gerichte gegevens worden aangepast aan de analysegegevens via SDID en worden verwerkt in de analytische rapporteringsopslag. De analysegegevens kunnen dan zowel in Analytics als [!DNL Target] via [!UICONTROL Analytics for Target] (A4T) rapporten worden bekeken. |

### Alleen op apparaat

Alleen op het apparaat is de beslissingsmethode die moet worden ingesteld in at.js 2.5.0+ wanneer [!UICONTROL on-device decisioning] alleen moet worden gebruikt op alle webpagina&#39;s.

[!UICONTROL On-device decisioning] kan uw ervaringen en personalisatieactiviteiten op een razendsnelle manier aanbieden, omdat de beslissingen worden genomen op basis van een cacheovereenkomst die al uw activiteiten bevat die in aanmerking komen voor [!UICONTROL on-device decisioning] .

Zie [!UICONTROL on-device decisioning] Ondersteunde functies in [&#x200B; voor meer informatie over welke activiteiten in aanmerking komen voor [!UICONTROL on-device decisioning]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md) .

Deze besluitvormingsmethode zou slechts moeten worden gebruikt als de prestaties hoogst kritiek over alle pagina&#39;s zijn die besluiten van Doel vereisen. Houd er bovendien rekening mee dat wanneer deze beslissingsmethode wordt geselecteerd, uw [!DNL Target] -activiteiten die niet in aanmerking komen voor [!UICONTROL on-device decisioning] niet worden uitgevoerd of uitgevoerd. De bibliotheek at.js 2.5.0+ wordt gevormd om het caching regelartefact slechts te zoeken om besluiten te nemen.

In het volgende diagram ziet u de interactie tussen uw bezoeker, de browser, at.js 2.5.0+ en de CDN van Akamai. De Akamai CDN slaat het artefact van de regels voor het eerste bezoek van de bezoeker in het voorgeheugen op. Voor het eerste paginabezoek voor een nieuwe bezoeker, moet het artefact van de JSON- regels van Akamai CDN worden gedownload om plaatselijk op browser van de bezoeker in het voorgeheugen onder te brengen. Nadat het artefact van JSON-regels is gedownload, wordt de beslissing onmiddellijk genomen zonder een blokkerende netwerkaanroep. In het volgende stroomdiagram worden nieuwe bezoekers vastgelegd.

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![&#x200B; Op-apparaat slechts stroomdiagram &#x200B;](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/on-device-only.png " op-apparaat slechts stroomdiagram "){zoomable="yes"}

De volgende lijst komt overeen met de cijfers in het diagram:

>[!NOTE]
>
>[!DNL Adobe Target] Admin-servers kwalificeren al uw activiteiten die in aanmerking komen voor [!UICONTROL on-device decisioning] , genereren het Artefact van de JSON-regels en geven dit door aan de Akamai CDN. Uw activiteiten worden voortdurend gecontroleerd op updates om een nieuw Artefact van JSON-regels uit te voeren dat aan Akamai CDN moet worden doorgegeven.

| Stap | Beschrijving |
| --- | --- |
| 1 | De identiteitskaart van de Bezoeker van Experience Cloud wordt teruggewonnen van de [&#x200B; Dienst van de Identiteit van Adobe Experience Cloud &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=nl-NL). |
| 2 | De bibliotheek at.js wordt synchroon geladen en de hoofdtekst van het document verborgen.<br /> de bibliotheek at.js kan ook asynchroon met een facultatief pre-verbergend die fragment worden geladen op de pagina wordt uitgevoerd. |
| 3 | De bibliotheek at.js verbergt het lichaam om flikkering te voorkomen. |
| 4 | De bibliotheek at.js vraagt om het JSON-regelartefact van de dichtstbijzijnde Akamai CDN naar de bezoeker op te halen. |
| 5 | De Akamai CDN reageert met het Artefact van de JSON-regel. |
| 6 | De JSON-regelartefact wordt lokaal in de browser van de bezoeker in cache geplaatst. |
| 7 | De bibliotheek at.js interpreteert het JSON-regelartefact en voert het besluit uit om de ervaring op te halen en verbergt de geteste elementen. |
| 8 | De bibliotheek at.js toont het lichaam zodat de rest van de pagina voor uw bezoeker aan mening kan worden geladen. |
| 9 | De bibliotheek at.js manipuleert DOM om de ervaring van het caching JSON regelartefact terug te geven. |
| 10 | De ervaring wordt weergegeven voor de bezoeker. |
| 11 | De hele webpagina wordt geladen. |
| 12 | De analysegegevens worden verzonden naar de servers van de Inzameling van Gegevens. De gerichte gegevens worden aangepast aan de analysegegevens via SDID en worden verwerkt in de analytische rapporteringsopslag. De analysegegevens kunnen dan zowel in Analytics als [!DNL Target] via [!UICONTROL Analytics for Target] (A4T) rapporten worden bekeken. |

In het volgende diagram ziet u de interactie tussen uw bezoeker, de browser, op .js 2.5.0+ en de JSON-regelartefact in de cache voor het volgende paginahit of terugkerend bezoek van de bezoeker. Omdat het artefact van JSON-regels al in het cachegeheugen is opgeslagen en beschikbaar is in de browser, wordt de beslissing onmiddellijk genomen zonder een blokkerende netwerkaanroep. Dit stroomdiagram legt volgende paginanavigatie of terugkerende bezoekers vast.

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![&#x200B; op-apparaat slechts stroomdiagram voor verdere paginanavigatie en herhaal bezoeken &#x200B;](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/on-device-only-subsequent.png " slechts stroomdiagram op-apparaat voor verdere paginanavigatie en herhaal bezoeken "){zoomable="yes"}

De volgende lijst komt overeen met de cijfers in het diagram:

>[!NOTE]
>
>[!DNL Adobe Target] Admin-servers kwalificeren al uw activiteiten die in aanmerking komen voor [!UICONTROL on-device decisioning] , genereren het Artefact van de JSON-regels en geven dit door aan de Akamai CDN. Uw activiteiten worden voortdurend gecontroleerd op updates om een nieuw Artefact van JSON-regels uit te voeren dat aan Akamai CDN moet worden doorgegeven.

| Stap | Beschrijving |
| --- | --- |
| 1 | De identiteitskaart van de Bezoeker van Experience Cloud wordt teruggewonnen van de [&#x200B; Dienst van de Identiteit van Adobe Experience Cloud &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=nl-NL). |
| 2 | De bibliotheek at.js wordt synchroon geladen en de hoofdtekst van het document verborgen.<br /> de bibliotheek at.js kan ook asynchroon met een facultatief pre-verbergend die fragment worden geladen op de pagina wordt uitgevoerd. |
| 3 | De bibliotheek at.js verbergt het lichaam om flikkering te voorkomen. |
| 4 | De bibliotheek at.js interpreteert het JSON-regelartefact en voert de beslissing in het geheugen uit om de ervaring op te halen. |
| 5 | De geteste elementen zijn verborgen. |
| 6 | De bibliotheek at.js toont het lichaam zodat de rest van de pagina voor uw bezoeker aan mening kan worden geladen. |
| 7 | De bibliotheek at.js manipuleert DOM om de ervaring van het caching JSON regelartefact terug te geven. |
| 8 | De ervaring wordt weergegeven voor de bezoeker. |
| 9 | De hele webpagina wordt geladen. |
| 10 | De analysegegevens worden verzonden naar de servers van de Inzameling van Gegevens. De gerichte gegevens worden aangepast aan de analysegegevens via SDID en worden verwerkt in de analytische rapporteringsopslag. De analysegegevens kunnen dan zowel in Analytics als [!DNL Target] via [!UICONTROL Analytics for Target] (A4T) rapporten worden bekeken. |

### Hybride

Hybride is de beslissingsmethode die moet worden ingesteld in at.js 2.5.0+ wanneer zowel [!UICONTROL on-device decisioning] als activiteiten die een netwerkaanroep naar het [!DNL Adobe Target] Edge-netwerk vereisen, moeten worden uitgevoerd.

Wanneer u zowel [!UICONTROL on-device decisioning] -activiteiten als serveractiviteiten beheert, kan dit een beetje ingewikkeld en vervelend zijn wanneer u nadenkt over het implementeren en plaatsen van [!DNL Target] op uw pagina&#39;s. Met hybride methoden als de beslissingsmethode weet [!DNL Target] wanneer een server moet worden aangeroepen naar het [!DNL Adobe Target] Edge-netwerk voor activiteiten die uitvoering op de server vereisen, en ook wanneer alleen beslissingen op het apparaat moeten worden uitgevoerd.

Het Artefact van de JSON-regels bevat metagegevens om at.js te laten weten of een box een serveractiviteit heeft die wordt uitgevoerd of een [!UICONTROL on-device decisioning] -activiteit. Deze beslissingsmethode zorgt ervoor dat activiteiten die u snel wilt laten uitvoeren, worden uitgevoerd via [!UICONTROL on-device decisioning] en voor activiteiten die krachtigere, door ML gestuurde personalisatie vereisen, worden deze activiteiten uitgevoerd via het [!DNL Adobe Target] Edge-netwerk.

In het volgende diagram ziet u de interactie tussen uw bezoeker, de browser, op .js 2.5.0+, de Akamai CDN en de [!DNL Adobe Target] Edge Network voor een nieuwe bezoeker die uw pagina voor het eerst bezoekt. Het weghalen van dit diagram is dat het artefact van de JSON-regels asynchroon wordt gedownload terwijl de beslissingen via het [!DNL Adobe Target] Edge-netwerk worden genomen.

Deze benadering zorgt ervoor dat de grootte van het artefact, dat vele activiteiten kan omvatten, niet negatief de latentie van de beslissing beïnvloedt. Het synchroon downloaden van de JSON-regels en het vervolgens nemen van de beslissing kan ook negatieve gevolgen hebben voor de latentie en kan inconsistent zijn. Daarom is de hybride besluitvormingsmethode een beste praktijkaanbeveling om altijd een server-zijvraag voor het besluit voor een nieuwe bezoeker te maken, en aangezien de JSON regels artefact parallel in het voorgeheugen wordt opgeslagen. Voor om het even welke verdere paginabezoeken en terugkeerbezoeken, worden de besluiten genomen van het geheime voorgeheugen en in geheugen door het JSON regelartefact.

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![&#x200B; Hybrid stroomdiagram voor een eerste-tijdbezoeker &#x200B;](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/hybrid-first-time-visitor.png " Hybrid stroomdiagram voor een eerste-tijdbezoeker "){zoomable="yes"}

De volgende lijst komt overeen met de cijfers in het diagram:

>[!NOTE]
>
>[!DNL Adobe Target] Admin-servers kwalificeren al uw activiteiten die in aanmerking komen voor [!UICONTROL on-device decisioning] , genereren het Artefact van de JSON-regels en geven dit door aan de Akamai CDN. Uw activiteiten worden voortdurend gecontroleerd op updates om een nieuw Artefact van JSON-regels uit te voeren dat aan Akamai CDN moet worden doorgegeven.

| Stap | Beschrijving |
| --- | --- |
| 1 | De identiteitskaart van de Bezoeker van Experience Cloud wordt teruggewonnen van de [&#x200B; Dienst van de Identiteit van Adobe Experience Cloud &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=nl-NL). |
| 2 | De bibliotheek at.js wordt synchroon geladen en de hoofdtekst van het document verborgen.<br /> de bibliotheek at.js kan ook asynchroon met een facultatief pre-verbergend die fragment worden geladen op de pagina wordt uitgevoerd. |
| 3 | De bibliotheek at.js verbergt het lichaam om flikkering te voorkomen. |
| 4 | Er wordt een aanvraag ingediend om de pagina te laden naar de Edge Network van [!DNL Adobe Target] , inclusief alle geconfigureerde parameters zoals (ECID, Customer ID, Custom Parameters, User Profile, enzovoort.) |
| 5 | Parallel hieraan vraagt at.js om het Artefact van de JSON-regel van de dichtstbijzijnde Akamai CDN naar de bezoeker op te halen. |
| 6 | ([!DNL Adobe Target] Edge Network) Profielscripts worden uitgevoerd en vervolgens toegevoegd aan de profielenwinkel. In de profielopslag wordt een gekwalificeerd publiek aangevraagd vanuit de publieksbibliotheek (bijvoorbeeld een publiek dat wordt gedeeld vanuit Adobe Analytics, Adobe Audience Manager enzovoort). |
| 7 | De Akamai CDN reageert met het Artefact van de JSON-regel. |
| 8 | De profielenopslag wordt gebruikt voor publiekskwalificatie en het opnemen aan filteractiviteiten. |
| 9 | De resulterende inhoud wordt geselecteerd nadat de ervaring is bepaald op basis van live [!DNL Target] -activiteiten. |
| 10 | De bibliotheek at.js verbergt de overeenkomstige elementen op de pagina die aan de ervaring worden geassocieerd die moet worden teruggegeven. |
| 11 | De bibliotheek at.js toont het lichaam zodat de rest van de pagina voor uw bezoeker aan mening kan worden geladen. |
| 12 | De bibliotheek at.js manipuleert de DOM om de ervaring van [!DNL Target] Edge Network terug te geven. |
| 13 | De ervaring wordt weergegeven voor de bezoeker. |
| 14 | De hele webpagina wordt geladen. |
| 15 | De analysegegevens worden verzonden naar de servers van de Inzameling van Gegevens. De gerichte gegevens worden aangepast aan de analysegegevens via SDID en worden verwerkt in de analytische rapporteringsopslag. De analysegegevens kunnen dan zowel in Analytics als [!DNL Target] via [!UICONTROL Analytics for Target] (A4T) rapporten worden bekeken. |

Het volgende diagram illustreert de interactie tussen uw bezoeker, browser, at.js 2.5.0+, en het caching JSON regelt artefact voor een verdere paginanavigatie of een terugkeerbezoek. In dit diagram, concentreert zich slechts op het gebruiksgeval dat een op-apparatenbesluit voor de verdere paginanavigatie of terugkeerbezoek wordt genomen. Houd in mening dat afhankelijk van welke activiteiten voor bepaalde pagina&#39;s levend zijn, een server-zijvraag kan worden gemaakt om server-zijbesluiten uit te voeren.

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![&#x200B; Hybrid stroomdiagram voor verdere paginanavigatie en herhaal bezoeken &#x200B;](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/hybrid-subsequent.png " Hybrid stroomdiagram voor verdere paginanavigatie en herhaal bezoeken "){zoomable="yes"}

De volgende lijst komt overeen met de cijfers in het diagram:

>[!NOTE]
>
>[!DNL Adobe Target] Admin-servers kwalificeren al uw activiteiten die in aanmerking komen voor [!UICONTROL on-device decisioning] , genereren het Artefact van de JSON-regels en geven dit door aan de Akamai CDN. Uw activiteiten worden voortdurend gecontroleerd op updates om een nieuw Artefact van JSON-regels uit te voeren dat aan Akamai CDN moet worden doorgegeven.

| Stap | Beschrijving |
| --- | --- |
| 1 | De identiteitskaart van de Bezoeker van Experience Cloud wordt teruggewonnen van de [&#x200B; Dienst van de Identiteit van Adobe Experience Cloud &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=nl-NL). |
| 2 | De bibliotheek at.js wordt synchroon geladen en de hoofdtekst van het document verborgen.<br /> de bibliotheek at.js kan ook asynchroon met een facultatief pre-verbergend die fragment worden geladen op de pagina wordt uitgevoerd. |
| 3 | De bibliotheek at.js verbergt het lichaam om flikkering te voorkomen. |
| 4 | Er wordt een verzoek ingediend om een ervaring op te halen. |
| 5 | De bibliotheek at.js bevestigt dat het JSON-regelartefact al in de cache is geplaatst en voert het besluit in het geheugen uit om de ervaring op te halen. |
| 6 | De geteste elementen zijn verborgen. |
| 7 | De bibliotheek at.js toont het lichaam zodat de rest van de pagina voor uw bezoeker aan mening kan worden geladen. |
| 8 | De bibliotheek at.js manipuleert DOM om de ervaring van het caching JSON regelartefact terug te geven. |
| 9 | De ervaring wordt weergegeven voor de bezoeker. |
| 10 | De hele webpagina wordt geladen. |
| 11 | De analysegegevens worden verzonden naar de servers van de Inzameling van Gegevens. De gerichte gegevens worden aangepast aan de analysegegevens via SDID en worden verwerkt in de analytische rapporteringsopslag. De analysegegevens kunnen dan zowel in Analytics als [!DNL Target] via [!UICONTROL Analytics for Target] (A4T) rapporten worden bekeken. |

## Hoe schakel ik [!UICONTROL on-device decisioning] in?

[!UICONTROL On-device decisioning] is beschikbaar voor alle [!DNL Target] -klanten die At.js 2.5.0+ gebruiken.

[!UICONTROL on-device decisioning] inschakelen:

>[!NOTE]
>
>U moet Admin of de Approver [&#x200B; gebruikersrol &#x200B;](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html?lang=nl-NL) hebben om de op-Apparaat van een knevel te voorzien of onbruikbaar te maken.

1. Klik op **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]**.
1. Schuif onder **[!UICONTROL Account details]** de schakeloptie **[!UICONTROL On-Device Decisioning]** naar de positie &quot;aan&quot;.

   ![[!UICONTROL On-device decisioning] toggle &#x200B;](assets/on-device-decisioning-toggle.png)

   De optie Alle bestaande [!UICONTROL on-device decisioning] gekwalificeerde activiteiten opnemen in het artefact wordt weergegeven als u [!UICONTROL on-device decisioning] inschakelt.
1. (Voorwaardelijk) Schuif de schakeloptie naar de positie &quot;aan&quot; als u wilt dat al uw live [!DNL Target] -activiteiten die voor [!UICONTROL on-device decisioning] in aanmerking komen, automatisch in het artefact worden opgenomen.

   Als u deze schakeloptie uitschakelt, moet u alle [!UICONTROL on-device decisioning] -activiteiten opnieuw maken en activeren, zodat deze worden opgenomen in het gegenereerde artefact voor regels. Met andere woorden, elke activiteit in live-toestand voordat de beslissingsschakeloptie op het apparaat wordt ingeschakeld, is niet opgenomen in het artefact van de regels.

Na het toelaten van de knevel van het Beslissen op apparaat, [!DNL Target] begint producerend en verspreidend [&#x200B; regelartefacten &#x200B;](/help/dev/implement/client-side/atjs/on-device-decisioning/rule-artifact.md) voor uw cliënt.

>[!WARNING]
>
>Zorg ervoor dat u de schakeloptie inschakelt voordat u de [!DNL Adobe Target] SDK voor gebruik van [!UICONTROL on-device decisioning] initialiseert. De regelartefacten moeten eerst worden gegenereerd en doorgegeven aan de Akamai CDN&#39;s, anders werkt [!UICONTROL on-device decisioning] niet. De propagatie kan vijf tot tien minuten voor het eerste regelartefact vergen om aan Akamai CDN te produceren en te verspreiden.

## Hoe configureer ik at.js 2.5.0+ voor gebruik van [!UICONTROL on-device decisioning]?

1. Klik op **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]**.
1. Onder **[!UICONTROL Implementation Methods]** > **[!UICONTROL Main Implementation Method]** klikt u op **[!UICONTROL Edit]** naast uw versie at.js (moet .js 2.5.0 of hoger zijn).

   ![&#x200B; geeft de Belangrijkste montages van de Methode van de Implementatie uit &#x200B;](assets/main-implementation-method.png)

   >[!WARNING]
   >
   >Voordat u deze standaardinstellingen wijzigt, raadpleegt u eerst de Client Care om te voorkomen dat de huidige implementatie wordt beïnvloed.

1. Selecteer de gewenste beslissingsmethode:

   * Alleen server
   * Alleen op apparaat
   * Hybride

   ![&#x200B; geeft bij.js montagespaneel uit &#x200B;](assets/global-settings.png)

### Algemene instellingen

U kunt een standaardbeslissingsmethode configureren voor alle [!DNL Target] -beslissingen. De verschillende besluitvormingsmethodes zijn server-kant slechts, slechts op apparaat, en Hybrid. De beslissingsmethode die is geselecteerd in de [!DNL Target] -gebruikersinterface, wordt geconfigureerd in `window.targetGlobalSettings` onder het veld `decisioningMethod` . Leer meer over `decisioningMethod` in [&#x200B; targetGlobalSettings () &#x200B;](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#decisioningmethod).

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

Als u `decisioningMethod` in `window.targetGlobalSettings` plaatst, maar `decisioningMethod` voor elk [!DNL Adobe Target] besluit volgens uw gebruiksgeval zou willen met voeten treden, kunt u deze procedure doen door `decisioningMethod` in At.js2.5.0+ [&#x200B; te specificeren getOffers () &#x200B;](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) vraag.

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
>Als u &quot;op apparaat&quot; of &quot;hybride&quot; wilt gebruiken als een beslissingsmethode in de aanroep getOffers(), moet u ervoor zorgen dat de algemene instelling `decisioningMethod` heeft als &quot;op apparaat&quot; of &quot;hybride&quot;. De bibliotheek at.js 2.5.0+ moet weten of om het Artefact van de regels JSON onmiddellijk na het laden op de pagina te downloaden en in het voorgeheugen onder te brengen. Als de besluitvormingsmethode voor het globale plaatsen aan &quot;server-kant&quot;wordt geplaatst, en &quot;op-apparaat&quot;of &quot;hybride&quot;besluitvormingsmethode wordt overgegaan in de getOffers () vraag, zou at.js 2.5.0+ niet het JSON regelartefact in het voorgeheugen ondergebracht hebben om uw op-apparatenbesluiten uit te voeren.

### Artefactcache TTL

Het doel vertegenwoordigt uw activiteiten die voor [!UICONTROL on-device decisioning] als artefact kwalificeren dat uit meta-gegevens, regels, en voorwaarden bestaat. Dit artefact wordt in het cachegeheugen opgeslagen op de Akamai CDN. Tijdens het eerste bezoek van uw gebruiker, downloadt browser van de gebruiker en caches het artefact dat uw [!UICONTROL on-device decisioning] activiteiten vertegenwoordigt.

Bij volgende bezoeken aan uw site controleert de browser automatisch of er een nieuwere versie van het artefact moet worden gedownload. Met deze controle wordt latentie toegevoegd. De Artefacache TTL definieert het aantal minuten dat de browser niet mag controleren op een bijgewerkt artefact sinds de laatste geslaagde download. Hoe langer het tijdsbestek, hoe beter de prestaties. Hoe korter het tijdkader, hoe beter de gegevens worden versnipperd, maar dit gaat ten koste van extra latentie.

## Hoe weet ik dat een activiteit [!UICONTROL on-device decisioning] in aanmerking komt?

Nadat u een activiteit creeert die [!UICONTROL on-device decisioning] in aanmerking komt, is een etiket dat Beslissingen op Apparaat Geschikt leest, zichtbaar in de pagina van het Overzicht van de activiteit.

![&#x200B; Op-Apparaat Beslissend In aanmerking komend etiket op de pagina van het Overzicht van de activiteit.](assets/on-device-decisioning-eligible-label.png)

Dit label betekent niet dat de activiteit altijd via [!UICONTROL on-device decisioning] wordt geleverd. Alleen wanneer at.js 2.5.0+ is geconfigureerd voor gebruik van [!UICONTROL on-device decisioning] , wordt deze activiteit op het apparaat uitgevoerd. Als at.js 2.5.0+ niet wordt gevormd om op-apparaat te gebruiken, dan zal deze activiteit nog via een servervraag worden geleverd die van at.js wordt gemaakt.

U kunt filteren voor alle activiteiten die [!UICONTROL on-device decisioning] in aanmerking komen op de pagina Activiteiten via het filter In aanmerking komende voor besluitvorming op het apparaat.

![&#x200B; Op Apparaat beslist Beleenbaar filter op de pagina van Activiteiten.](assets/on-device-decisioning-filter.png)

>[!NOTE]
>
>Nadat u een activiteit hebt gemaakt en geactiveerd die [!UICONTROL on-device decisioning] in aanmerking komt, kan het vijf tot tien minuten duren voordat deze wordt opgenomen in het vervorming van regels die wordt gegenereerd en doorgegeven aan het Akamai CDN-punt met voorkeuren.

## Overzicht van stappen om ervoor te zorgen dat mijn [!UICONTROL on-device decisioning] activiteiten via At.js 2.5.0+ worden geleverd?

1. Open de gebruikersinterface van [!DNL Adobe Target] en navigeer naar **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account Details]** om de **[!UICONTROL On-Device Decisioning]** -schakeloptie in te schakelen.
1. Schakel de **[!UICONTROL "Include all existing [!UICONTROL on-device decisioning] qualified activities in the artifact"]** -schakeloptie in.

   De eerste JSON-regels kunnen tot 10 minuten duren.

1. Maak en activeer een [&#x200B; type activiteit dat door [!UICONTROL on-device decisioning]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md) wordt ondersteund, en controleer of dit [!UICONTROL on-device decisioning] mogelijk is.
1. Stel de **[!UICONTROL Decisioning Method]** in op **[!UICONTROL "Hybrid"]** of **[!UICONTROL "On-device only"]** via de interface voor instellingen bij.js.
1. Download en implementeer At.js 2.5.0+ op uw pagina&#39;s.
