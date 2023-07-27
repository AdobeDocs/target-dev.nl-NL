---
keywords: at.js faq, at.js veelgestelde vragen, faq, flicker, loader, paginalader, cross domain, bestandsgrootte, bestandsgrootte, x-domain, at.js en mbox.js, x only, cross domain, safari, single page app, missing selectors, selectors, single page application, tt.omtrdc.net, spa, Adobe Experience Manager, AEM, ip address, httponly, Http Only, secure, ip, cookie domain
description: Lees antwoorden op veelgestelde vragen over de [!DNL Adobe Target] at.js JavaScript-bibliotheek.
title: Wat zijn algemene vragen en antwoorden over at.js?
feature: at.js
exl-id: 362ccc5b-8731-46c0-bc52-3e55c273e216
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '2884'
ht-degree: 0%

---

# om.js Veelgestelde Vragen

Antwoorden op veelgestelde vragen over de [!DNL Adobe Target] at.js JavaScript-bibliotheek.

## Wat zijn de voordelen om at.js tegenover mbox.js te gebruiken?

De bibliotheek at.js vervangt mbox.js. De bibliotheek mbox.js wordt niet meer ondersteund. Voor de meeste mensen biedt at.js echter voordelen ten opzichte van mbox.js.

Het bestand at.js verbetert onder andere de laadtijden voor webimplementaties, verbetert de beveiliging en biedt betere implementatieopties voor toepassingen van één pagina.

In het volgende diagram worden de prestaties bij het laden van een pagina geïllustreerd met mbox.js versus at.js.

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![Paginaprestatiediagram waarin mbox.js wordt vergeleken met at.js](/help/dev/implement/client-side/atjs/assets/atjs_versus_mboxjs.png "Paginaprestatiediagram waarin mbox.js wordt vergeleken met at.js"){zoomable=&quot;yes&quot;}

Zoals hierboven is geïllustreerd, is met mbox.js de pagina-inhoud pas na de gebeurtenis [!DNL Target] de vraag is volledig. Wanneer u at.js gebruikt, wordt pagina-inhoud geladen wanneer de [!DNL Target] de vraag wordt in werking gesteld en wacht niet tot de vraag volledig is.

## Wat is het effect van at.js en mbox.js op pagina-ladingstijd?

Veel klanten en consultants willen weten wat het effect is van at.js en mbox.js op de laadtijd van de pagina, vooral in de context van nieuwe gebruikers of terugkerende gebruikers. Jammer genoeg, is het moeilijk om concrete aantallen betreffende te meten en te geven hoe te.js of mbox.js pagina-ladingstijd wegens de implementatie van elke klant beïnvloeden.

Als de API voor bezoekers echter aanwezig is op de pagina, [!DNL Target] kan beter begrijpen hoe at.js en mbox.js pagina-lading tijd beïnvloeden.

>[!NOTE]
>
>De API van de Bezoeker en at.js of mbox.js hebben alleen invloed op de laadtijd van de pagina wanneer u de globale mbox gebruikt (vanwege de body-hide techniek). De regionale mboxes worden niet beïnvloed door de integratie van de Bezoeker API.

De volgende secties beschrijven de opeenvolging van acties voor nieuwe en terugkerende bezoekers:

### Nieuwe bezoekers

1. De bezoeker-API wordt geladen, geparseerd en uitgevoerd.
1. at.js / mbox.js wordt geladen, geparseerd en uitgevoerd.
1. Als de optie voor automatisch maken van globale mbox is ingeschakeld, wordt de optie [!DNL Target] JavaScript-bibliotheek:

   * Instantieert het object Visitor.
   * De [!DNL Target] De bibliotheek probeert de gegevens van de Experience Cloud Visitor-id op te halen.
   * Omdat deze bezoeker een nieuwe bezoeker is, leidt de bezoeker-API een aanvraag voor een ander domein in op demdex.net.
   * Nadat de gegevens van identiteitskaart van de Bezoeker van Experience Cloud worden teruggewonnen, een verzoek aan [!DNL Target] wordt afgegaan.

### Bezoekers terugsturen

1. De bezoeker-API wordt geladen, geparseerd en uitgevoerd.
1. at.js / mbox.js wordt geladen, geparseerd en uitgevoerd.
1. Als de optie voor automatisch maken van globale mbox is ingeschakeld, wordt de optie [!DNL Target] JavaScript-bibliotheek:

   * Instantieert het object Visitor.
   * De [!DNL Target] De bibliotheek probeert de gegevens van de Experience Cloud Visitor-id op te halen.
   * De bezoeker-API haalt gegevens op uit cookies.
   * Nadat de gegevens van identiteitskaart van de Bezoeker van Experience Cloud worden teruggewonnen, een verzoek aan [!DNL Target] wordt afgegaan.

>[!NOTE]
>
>Voor nieuwe bezoekers, wanneer de API voor bezoekers aanwezig is, [!DNL Target] moet over de draad veelvoudige tijden gaan om ervoor te zorgen dat [!DNL Target] aanvragen bevatten Experience Cloud Visitor ID-gegevens. Voor terugkerende bezoekers [!DNL Target] gaat over de draad slechts aan [!DNL Target] om de gepersonaliseerde inhoud op te halen.

## Waarom lijkt het alsof ik langzamere reactietijden na bevordering van een vorige versie van at.js aan versie 1.0.0 zie?

in.js versie 1.0.0 en hoger worden alle aanvragen parallel geactiveerd. Eerdere versies voeren de aanvragen opeenvolgend uit, wat betekent dat de aanvragen in een wachtrij worden geplaatst en [!DNL Target] wacht op eerste verzoek om te voltooien alvorens op het volgende verzoek over te gaan.

De manier vorige versies van at.js verzoeken uitvoeren is vatbaar voor de zogenaamde &quot;hoofd van lijn het blokkeren.&quot; In at.js 1.0.0 en hoger [!DNL Target] geschakeld naar parallelle uitvoering van aanvragen.

Als u de waterval van het netwerklusje voor at.js 0.9.1 controleert, bijvoorbeeld, zult u dat volgende zien [!DNL Target] De aanvraag start pas nadat de vorige is voltooid. Deze volgorde is niet het geval bij at.js 1.0.0 en later, waar alle aanvragen eigenlijk tegelijkertijd beginnen.

Vanuit het perspectief van de reactietijd, wiskundig, kan deze opeenvolging als dit worden samengevoegd

<ul class="simplelist"> 
 <li> om.js 0.9.1: Reactietijd van allen [!DNL Target] verzoeken = som van verzoeken, reactietijd </li> 
 <li> om.js 1.0.0 en later: Reactietijd van allen [!DNL Target] verzoeken = maximum van verzoeken reactietijd </li> 
</ul>

Met versie 1.0.0 van de bibliotheek at.js worden de aanvragen sneller afgehandeld. Daarnaast zijn aanvragen van het type at.js asynchroon, dus [!DNL Target] blokkeert niet het weergeven van pagina&#39;s. Zelfs als verzoeken seconden duren, wordt de weergegeven pagina nog steeds weergegeven, maar enkele delen van de pagina worden gewist tot [!DNL Target] krijgt een antwoord van [!DNL Target] rand.

## Kan ik de [!DNL Target] asynchroon bibliotheek?

Met de release van at.js 1.0.0 kunt u de [!DNL Target] bibliotheek asynchroon.

Zo laadt u at.js asynchroon:

* De aanbevolen aanpak is via tags in Adobe Experience Platform.
* U kunt ook asynchroon laden bij .js door het asynchrone attribuut aan de manuscriptmarkering toe te voegen die at.js laadt. Gebruik iets als dit:

  ```
  <script src="<URL to at.js>" async></script>
  ```

* U kunt ook asynchroon laden bij .js met deze code:

  ```
  var script = document.createElement('script'); 
  script.async = true; 
  script.src = "<URL to at.js>"; 
  document.head.appendChild(script);
  ```

Het asynchroon laden bij.js is een goede manier om te voorkomen dat de browser wordt geblokkeerd bij het renderen. Deze techniek kan echter leiden tot flikkering op de webpagina.

U kunt flikkering vermijden door een vooraf verborgen fragment te gebruiken dat de pagina (of gespecificeerde gedeelten) verbergt en het dan onthult nadat om.js en het globale verzoek hebben geladen. Het fragment moet worden toegevoegd voordat u het bestand at.js laadt.

Als u at.js door asynchroon opstelt [!UICONTROL Adobe Experience Platform] implementatie, zorg ervoor dat u het vooraf verborgen fragment direct op uw pagina&#39;s opneemt, voordat u het implementeert [!DNL Target] gebruiken [!UICONTROL Adobe Experience Platform] Code insluiten.

Als u at.js door een synchrone implementatie DTM opstelt, kan het pre-verbergende fragment worden toegevoegd door een lijn van de Lading van de Pagina die bij de bovenkant van de pagina wordt teweeggebracht.

Zie voor meer informatie [Hoe at.js flikkering beheert](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md).

## Is at.js compatibel met [!DNL Adobe Experience Manager] integratie (Experience Manager)?

[!DNL Adobe Experience Manager] 6.2 met FP-11577 (of later) steunt nu bij.js implementaties met zijn [!UICONTROL Adobe Target Cloud Services] integratie.

## Hoe kan ik flikkering tijdens het laden van pagina&#39;s voorkomen met at.js?

[!DNL Target] biedt verschillende manieren om flikkering bij het laden van pagina&#39;s te voorkomen. Zie voor meer informatie [Flikkering voorkomen met at.js](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md).

## Wat is de bestandsgrootte van at.js?

Het bestand at.js is ongeveer 109 kB wanneer het wordt gedownload. Omdat de meeste servers bestanden echter automatisch comprimeren om de bestandsgrootte te verkleinen, is at.js ongeveer 34 kB bij het comprimeren (met GZIP of een andere methode) op uw server en het laden als gebruikers uw website bezoeken. De compressie-instellingen op de server waarop u .js hebt geïnstalleerd, bepalen de werkelijke gecomprimeerde grootte.

## Waarom is at.js groter dan mbox.js?

bij.js de implementaties gebruiken één enkele bibliotheek ( at.js), terwijl mbox.js de implementaties eigenlijk twee bibliotheken ( mbox.js en target.js) gebruiken. Een eerlijkere vergelijking is dus at.js versus mbox.js *en* `target.js`. Wanneer de gecomprimeerde grootte van de twee versies wordt vergeleken, is versie 1.js 1.2 34 kB en versie 63 mbox.js 26,2 kB. &quot;

at.js is groter omdat het veel meer DOM ontleedt in vergelijking met mbox.js. Dit is vereist omdat at.js &quot;onbewerkte&quot;gegevens in de reactie JSON krijgt en het moet zinvol maken. mbox.js gebruikt `document.write()` en al het parseren werd gedaan door browser.

Ondanks de grotere bestandsgrootte geven onze tests aan dat pagina&#39;s sneller worden geladen met at.js versus mbox.js. Ook, is at.js superieur vanuit veiligheidsperspectief omdat het geen extra dossiers dynamisch laadt of gebruikt `document.write`.

## Heeft at.js er jQuery in? Kan ik dit deel van at.js verwijderen omdat ik al jQuery op mijn website heb?

at.js gebruikt momenteel delen van jQuery en dus ziet u de MIT-licentiemelding boven aan at.js. jQuery wordt niet weergegeven en heeft geen invloed op de jQuery-bibliotheek die u al op de pagina hebt, wat een andere versie kan zijn. Het verwijderen van de jQuery-code in at.js wordt niet ondersteund.

## Biedt at.js ondersteuning voor Safari en cross domain ingesteld op x-only?

Nee, als cross-domain is ingesteld op x-only en Safari cookies van derden heeft uitgeschakeld, wordt zowel mbox.js als at.js een uitgeschakelde cookie ingesteld en worden geen box-aanvragen uitgevoerd voor het domein van die client.

Om Safari bezoekers te ondersteunen, zou een beter X-Domein &quot;gehandicapt&quot;zijn (plaatst slechts een eerste-partijkoekje) of &quot;toegelaten&quot;(plaatst slechts een eerste-partijkoekje op Safari, terwijl het plaatsen van eerste en derdekoekjes op andere browsers).

## Kan ik het doel gebruiken [!UICONTROL Visual Experience Composer] (VEC) in mijn toepassingen van één pagina?

Ja, u kunt VEC voor uw SPA gebruiken als u at.js 2.x gebruikt. Zie voor meer informatie [Single Page (SPA) Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/spa-visual-experience-composer.html).

## Kan ik de Adobe Experience Cloud Debugger gebruiken met at.js implementaties?

Ja. U kunt mboxTrace voor het zuiveren doeleinden of de Hulpmiddelen van de Ontwikkelaar van uw browser ook gebruiken om de verzoeken van het Netwerk te inspecteren, filtrerend aan &quot;mbox&quot;om mbox vraag te isoleren.

## Kan ik speciale karakters in mbox namen met at.js gebruiken?

Ja, hetzelfde als met mbox.js.

## Waarom worden mijn dozen niet op mijn webpagina&#39;s geactiveerd?

[!DNL Target] klanten gebruiken soms cloudgebaseerde instanties met [!DNL Target] voor tests of eenvoudige concepttest. Deze en vele andere domeinen maken deel uit van de [Lijst met openbare achtervoegsels](https://publicsuffix.org/list/public_suffix_list.dat).

Moderne browsers slaan cookies niet op als u deze domeinen gebruikt, tenzij u de opties `cookieDomain` instellen met targetGlobalSettings(). Zie voor meer informatie [Op cloud gebaseerde instanties gebruiken met [!DNL Target]](/help/dev/implement/client-side/target-debugging-atjs/targeting-using-cloud-based-instances.md).

## Kunnen IP adressen als koekjesdomein worden gebruikt wanneer het gebruiken van at.js?

Ja, als u [at.js versie 1.2 of hoger](/help/dev/implement/client-side/atjs/target-atjs-versions.md). Adobe raadt u echter ten zeerste aan de nieuwste versie bij te houden.

>[!NOTE]
>
>De volgende voorbeelden zijn niet nodig als u at.js versie 1.2 of later gebruikt.

Afhankelijk van hoe u [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md), moet u mogelijk aanvullende wijzigingen in de code aanbrengen nadat u het bestand at.js hebt gedownload. Als u bijvoorbeeld iets andere instellingen voor uw [!DNL Target] implementaties op verschillende websites die deze instellingen niet dynamisch kunnen definiëren met behulp van aangepaste JavaScript, deze aanpassingen handmatig uitvoeren nadat het bestand is gedownload en voordat het bestand naar de desbetreffende website wordt geüpload.

In de volgende voorbeelden kunt u de `targetGlobalSettings()` de functie at.js om een codefragment op te nemen om IP adressen te steunen:

Dit voorbeeld is voor één enkel IP adres:

```
if (window.location.hostname === '123.456.78.9') { 
    window.targetGlobalSettings = window.targetGlobalSettings || {}; 
    window.targetGlobalSettings.cookieDomain = window.location.hostname; 
}
```

Dit voorbeeld is voor een waaier van IP adressen:

```
if (/^123\.456\.78\..*/g.test(window.location.hostname)) { 
    window.targetGlobalSettings = window.targetGlobalSettings || {}; 
    window.targetGlobalSettings.cookieDomain = window.location.hostname; 
}
```

## Waarom zie ik waarschuwingsberichten, zoals &quot;acties met ontbrekende kiezers&quot;?

Deze berichten hebben geen betrekking op de functionaliteit at.js. De bibliotheek at.js probeert om het even wat te melden die niet in DOM kan worden gevonden.

Als dit waarschuwingsbericht wordt weergegeven, zijn de volgende mogelijke hoofdoorzaken:

* De pagina wordt dynamisch samengesteld en at.js kan het element niet vinden.
* De pagina wordt langzaam gebouwd (wegens een langzaam netwerk) en at.js kan niet de selecteur in DOM vinden.
* De paginastructuur waarop de activiteit wordt uitgevoerd, is gewijzigd. Als u de activiteit in de Visuele Composer van de Ervaring (VEC) heropent, zou u een waarschuwingsbericht moeten krijgen. Werk de activiteit bij zodat alle noodzakelijke elementen kunnen worden gevonden.
* De onderliggende pagina maakt deel uit van een toepassing voor één pagina (SPA) of de pagina bevat elementen die verder naar beneden op de pagina worden weergegeven en het &#39;opiniepeilingsmechanisme&#39; van at.js kan die elementen niet vinden. De `selectorsPollingTimeout` zou kunnen helpen. Zie voor meer informatie [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).
* Om het even welke klik-volgende metrisch probeert om aan elke pagina toe te voegen, ongeacht URL waarop metrisch opstelling was. Hoewel onschuldig, maakt deze situatie veel van deze berichten tonen.

  Download en gebruik de [nieuwste versie van at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md). Voor meer informatie over het downloaden van at.js raadpleegt u de [Download om.js met de [!DNL Target] interface](how-to-deployatjs/implement-target-without-a-tag-manager.md#download-atjs-using-the-target-interface) in de [*Hoe te opstellen bij.js* > *Implementeren [!DNL Target] zonder tagbeheer*](how-to-deployatjs/implement-target-without-a-tag-manager.md) artikel.

## Wat is het domein tt.omtrdc.net dat [!DNL Target] serveraanroepen gaan naar?

tt.omtrdc.net is de domeinnaam voor Adobe EDGE netwerk, dat wordt gebruikt om alle servervraag te ontvangen [!DNL Target].

## Waarom gebruikt at.js altijd vlaggen van het Toegangske- en Veilige koekje HttpOnly?

HttpOnly kan alleen worden ingesteld via code op de server. [!DNL Target] cookies, zoals mbox, worden gemaakt en opgeslagen via JavaScript-code, zodat [!DNL Target] Kan de koekjesvlag niet gebruiken HttpOnly. [!DNL Target] Hierbij wordt HttpOnly ingesteld voor cookies van derden die vanaf de server worden ingesteld wanneer cross-domain is ingeschakeld.

Beveiliging kan alleen via JavaScript worden ingesteld wanneer de pagina via HTTPS is geladen. Als de pagina voor het eerst wordt geladen via HTTP, kan JavaScript deze markering niet instellen. Als de markering Beveiligen wordt gebruikt, is de cookie bovendien alleen beschikbaar op HTTPS-pagina&#39;s. Voor pagina&#39;s die via HTTPS worden geladen, [!DNL Target] Hiermee worden de kenmerken Secure en SameSite=None ingesteld.

Om ervoor te zorgen dat [!DNL Target] gebruikers goed kunnen volgen en omdat de cookies op de client worden gegenereerd, [!DNL Target] gebruikt geen van beide vlaggen behalve in de hierboven vermelde situaties.

## Hoe behandelt at.js veiligheidskwesties zoals aanvallen XSS en MITM?

Communicatie met het Adobe Edge-netwerk, ingeschakeld door at.js, vindt alleen plaats via HTTPS zolang de `secureOnly` option is ingesteld op true in de targetGlobalSettings() functie ([targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)), anders is at.js toegestaan tussen HTTP en HTTPS te schakelen op basis van het paginaprotocol.

De volgende headers worden standaard afgedwongen:
* HTTP Strict Transport Security (HSTS)
* X-XSS-beveiliging
* Opties voor X-inhoudstype
* Referrer-Policy

Alle kopteksten die al in cliëntpagina&#39;s worden gebruikt kunnen worden afgedwongen. Een algemene manier om dit te doen is door &quot;HTTP-aanvraagheaderautorisatie&quot;. De klantenservice van Adobe kan advies geven over de beste methoden en praktijken.

Bovendien zijn verzoeken aan het Adobe Edge-netwerk openbaar (omdat ze ontworpen zijn om te worden gemaakt vanuit browsers van bezoekers) en bevatten ze geen zichtbare bezoekersgegevens (ze bevatten alleen een bezoekersidentiteitskaart). Deze verzoeken bieden bezoekers ervaringen en bevatten informatie over wat een bezoeker op de pagina moet zien.

Merk op dat voor reactietokens en zitting IDs die in deze verzoeken worden overgebracht:

* Ze houden communicatiesessies bij
* Ze bestaan uit willekeurige tekens
* Sessie-id&#39;s zijn 30 minuten geldig
* Responstokens kunnen worden uitgeschakeld ([Reactietokens](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html))
* Ze zijn alleen nuttig in de omgeving van Adobe-oplossingen.

Verwacht wordt dat de `Access-Control-Allow-Origin` header met de waarde &quot;*&quot; in at.js-aanvragen, omdat ze openbaar zijn, is verificatie niet vereist en moet het Adobe Edge-netwerk via JavaScript-aanroepen vanuit elk domein worden benaderd.

Het inhoudsbeveiligingsbeleid (CSP) moet echter op de pagina worden afgedwongen. Zie voor meer informatie over CSP-vereisten voor at.js [Beveiligingsbeleid voor inhoud](/help/dev/before-implement/privacy/content-security-policy.md) en [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

## Hoe vaak leidt at.js een netwerkverzoek in brand?

[!DNL Target] voert al zijn besluit op de server uit. Dit betekent dat at.js elke keer dat de pagina opnieuw wordt geladen of een openbare API van at.js wordt aangeroepen, een netwerkverzoek in werking stelt.

## In het beste geval, kunnen wij verwachten dat de gebruiker geen zichtbare gevolgen op paginading met betrekking tot het verbergen van, het vervangen van, en het tonen van inhoud ervaart?

at.js probeert pre-verbergen HTML BODY of andere DOM elementen voor een langere periode te vermijden, maar dit hangt van netwerkvoorwaarden en activiteitenopstelling af. at.js biedt [instellingen](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) U kunt de LICHAAM die CSS-stijl verbergt, aanpassen, zodat u in plaats van de hele HTML BODY te lekken, slechts enkele delen van de pagina kunt voorverbergen. De verwachting is dat die onderdelen DOM-elementen bevatten die &quot;gepersonaliseerd&quot; moeten worden.

## Wat is de opeenvolging van gebeurtenissen in een gemiddeld scenario waar een gebruiker voor een activiteit kwalificeert?

Het verzoek at.js is een asynchroon `XMLHttpRequest`, dus voeren we de volgende stappen uit:

1. De pagina wordt geladen.
1. at.js prehides the HTML BODY. Er is een instelling voor het vooraf verbergen van een bepaalde container in plaats van de HTML BODY.
1. De aanvraag at.js wordt geactiveerd.
1. Na de [!DNL Target] antwoord ontvangen; [!DNL Target] Hiermee worden de CSS-kiezers uitgepakt.
1. CSS-kiezers gebruiken [!DNL Target] maakt STIJL-tags om de DOM-elementen die worden aangepast, vooraf te verbergen.
1. De vooraf verborgen STIJL voor het HTML-LICHAAM wordt verwijderd.
1. [!DNL Target] start opiniepeiling voor DOM-elementen.
1. Als een DOM-element wordt gevonden, [!DNL Target] past DOM-wijzigingen toe en de vooraf verborgen STIJL van het element wordt verwijderd.
1. Als DOM-elementen niet worden gevonden, verbergt een algemene time-out de elementen om te voorkomen dat een pagina wordt verbroken.

## Hoe vaak wordt de inhoud van de pagina volledig geladen en zichtbaar wanneer at.js definitief het element ontverbergt de activiteit verandert?

Gezien het bovenstaande scenario, hoe vaak wordt de inhoud van de pagina volledig geladen en zichtbaar wanneer at.js definitief het element ontverbergt de activiteit verandert? Met andere woorden, de pagina is volledig zichtbaar behalve de inhoud van de activiteit, die dan lichtjes na de rest van de inhoud wordt onthuld.

at.js blokkeert niet dat de pagina wordt weergegeven. Een gebruiker kan enkele lege gebieden op de pagina opmerken die elementen vertegenwoordigen die zijn aangepast door [!DNL Target]. Als de toe te passen inhoud niet vele verre activa, zoals SCRIPTs of IMGs bevat, zou alles snel moeten teruggeven.

## Hoe zou een volledig caching pagina het bovengenoemde scenario beïnvloeden? Zou het waarschijnlijker zijn dat de inhoud van de activiteit merkbaar zichtbaar wordt nadat de rest inhoud van de pagina laadt?

Als een pagina in de cache wordt geplaatst op een CDN die dicht bij de locatie van de gebruiker staat, maar niet bij de locatie [!DNL Target] Edge, kan de gebruiker enige vertragingen zien. [!DNL Target] de randen zijn over de hele wereld goed verdeeld , dus dit is niet de meeste tijd een probleem .

## Is het mogelijk dat een hoofdafbeelding na een korte vertraging wordt weergegeven en vervolgens wordt omgewisseld?

Met het volgende scenario:

De [!DNL Target] time-out is vijf seconden. Een gebruiker laadt een pagina die een activiteit heeft om een hoofdafbeelding aan te passen. at.js verzendt het verzoek om te bepalen als er een activiteit is om toe te passen, maar er is geen aanvankelijke reactie. Stel dat de gebruiker de reguliere inhoud van de hoofdafbeelding ziet, omdat er geen reactie is ontvangen van [!DNL Target] met betrekking tot de vraag of er een verwante activiteit is. Na vier seconden [!DNL Target] retourneert een reactie met de inhoud van de activiteit.

Zou het in dit stadium mogelijk zijn de alternatieve versie te tonen? Na vier seconden kon de hoofdafbeelding worden omgewisseld en kon de gebruiker deze afbeeldingswisseling zien?

In eerste instantie is het DOM-element voor de held van de afbeelding verborgen. Na een reactie van [!DNL Target] ontvangen, past at.js de DOM-wijzigingen toe, zoals het vervangen van de IMG en het weergeven van de aangepaste hoofdafbeelding.

## Welk HTML doctype vereist at.js?

at.js vereist het documenttype van HTML 5.

Deze syntaxis is:

`<!DOCTYPE html>`

Het documenttype HTML 5 zorgt ervoor dat de pagina in de standaardmodus wordt geladen. Bij het laden in de modus Kirken zijn sommige JS API&#39;s waarvan at.js afhankelijk is, uitgeschakeld. [!DNL Target] Schakelt in de modus kirken de modus at.js uit.
