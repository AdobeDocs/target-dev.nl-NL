---
keywords: implementatie van één pagina, toepassing van één pagina, spa, at.js 2.x, at.js, toepassing van één pagina, app van één pagina, spa, SPA, implementatie van één pagina-toepassing
description: Leren gebruiken [!DNL Adobe Target] om.js 2.x uit te voeren [!DNL Target] voor toepassingen voor één pagina (SPA).
title: Kan ik implementeren [!DNL Target] voor Single Page Applications (SPA)?
feature: Implement Server-side
exl-id: d59d7683-0a63-47a9-bbb5-0fe4a5bb7766
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '2767'
ht-degree: 1%

---

# Toepassing van één pagina

Traditionele websites werkten aan navigatiemodellen &quot;van pagina tot pagina&quot;, ook wel bekend als Toepassingen van meerdere pagina&#39;s, waarbij websiteontwerpen nauw gekoppeld waren aan URL&#39;s en overgangen van de ene webpagina naar de andere een pagina moesten laden. Moderne webtoepassingen, zoals Single Page Applications (SPA), maken in plaats daarvan gebruik van een model dat snel gebruik van de rendering van de gebruikersinterface van de browser aanmoedigt. Deze is vaak niet afhankelijk van het opnieuw laden van pagina&#39;s. Deze ervaringen worden vaak veroorzaakt door klanteninteractie, zoals scrolls, kliks, en curseurbewegingen. Naarmate de paradigma&#39;s van het moderne web zijn geëvolueerd, werkt de relevantie van traditionele generieke gebeurtenissen, zoals page-load, om personalisatie en experimenten te implementeren, niet meer.

![Traditionele levenscyclus van pagina&#39;s versus SPA levenscyclus](assets/trad-vs-spa.png)

at.js 2.x verstrekt rijke eigenschappen die uw zaken uitrusten om verpersoonlijking op volgende-generatie, cliënt-zijtechnologieën uit te voeren. Deze versie is gericht op het verbeteren van at.js om harmonieuze interactie met SPA te hebben.

Hier volgen enkele voordelen van het gebruik van at.js 2.x die niet beschikbaar zijn in eerdere versies:

* De capaciteit om alle aanbiedingen op pagina-lading in het voorgeheugen onder te brengen om veelvoudige servervraag aan één enkele servervraag te verminderen.
* Verbeter de ervaringen van uw eindgebruikers op uw site aanzienlijk, omdat aanbiedingen direct via de cache worden weergegeven zonder vertraging die door traditionele serveraanroepen wordt geïntroduceerd.
* Een eenvoudige one-line code en éénmalige ontwikkelaarsopstelling om uw marketers toe te laten om A/B en de Gerichte (XT) activiteiten van de Ervaring tot stand te brengen en in werking te stellen via VEC op uw SPA.

## [!DNL Adobe Target] Weergaven en toepassingen voor één pagina

De [!DNL Adobe Target] VEC voor SPA maakt gebruik van een nieuw concept genaamd Views: een logische groep visuele elementen die samen een SPA ervaring vormen. Een SPA kan daarom worden beschouwd als een overgang door weergaven in plaats van URL&#39;s, op basis van gebruikersinteracties. Een weergave kan doorgaans een hele site of gegroepeerde visuele elementen binnen een site vertegenwoordigen.

Als u meer wilt weten over de weergaven, navigeert u naar deze hypothetische online e-commercesite die u in Reageren hebt geïmplementeerd en verkent u enkele voorbeeldweergaven. Klik op de onderstaande koppelingen om deze site te openen in een nieuw browsertabblad.

**Koppeling: [Home Site](https://target.enablementadobe.com/react/demo/#/)**

![thuissite](assets/home.png)

Wanneer we naar de thuissite gaan, zien we meteen een hoofdafbeelding die een paasverkoop bevordert en de nieuwste producten die op de site worden verkocht. In dit geval, kan een Mening als volledige homesite worden gedefinieerd. Dit is handig om op te merken, aangezien we dit in de uitvoeringsfase verder zullen uitbreiden [!DNL Adobe Target] Sectie Weergaven verderop.

**Koppeling: [Productsite](https://target.enablementadobe.com/react/demo/#/products)**

![productsite](assets/product-site.png)

Aangezien wij meer in de producten worden geinteresseerd die de zaken verkopen, besluiten wij om de verbinding van Producten te klikken. Net als op de thuissite kan de hele productsite worden gedefinieerd als een weergave. Deze weergave kan net als de padnaam in `https://target.enablementadobe.com/react/demo/#/products)`.

![productsite 2](assets/product-site-2.png)

In het begin van deze sectie definieerden we Weergaven als de gehele site of zelfs als een groep visuele elementen op de site. Zoals hierboven wordt getoond, kunnen de vier producten die op de plaats worden getoond ook als Mening worden gegroepeerd en worden beschouwd. Als we deze weergave een naam willen geven, kunnen we het een product noemen.

![productsite 3](assets/product-site-3.png)

Klik op de knop Meer laden om meer producten op de site te verkennen. De URL van de website verandert in dit geval niet. Maar een weergave hier kan alleen de tweede rij producten weergeven die hierboven wordt weergegeven. De weergavenaam kan &#39;PRODUCTS-PAGE-2&#39; worden genoemd.

**Koppeling: [Afhandeling](https://target.enablementadobe.com/react/demo/#/checkout)**

![uitcheckpagina](assets/checkout.png)

Omdat we bepaalde producten op de site leuk vonden, besloten we een paar te kopen. Nu krijgen we op de uitchecksite enkele opties om normale levering of expreslevering te kiezen. Omdat een weergave elke groep visuele elementen op een site kan zijn, kunnen we deze &quot;Voorkeuren voor levering weergeven&quot; noemen.

Bovendien kan het concept van de standpunten veel verder worden uitgebreid. Als marketers de inhoud op de site willen aanpassen, afhankelijk van de geselecteerde leveringsvoorkeur, kan een Weergave worden gemaakt voor elke leveringsvoorkeur. In dit geval, wanneer wij Normale Levering selecteren, kan de Mening &quot;Normale Levering worden genoemd.&quot; Als Express Delivery is geselecteerd, kan de weergave de naam &quot;Express Delivery&quot; hebben.

Marktdeelnemers kunnen nu een A/B-test uitvoeren om te zien of het wijzigen van de kleur van blauw in rood wanneer Express Delivery is geselecteerd, conversies kan stimuleren in plaats van de knopkleur blauw te houden voor beide leveringsopties.

## Implementatie [!DNL Adobe Target] Weergaven

Nu hebben we het over [!DNL Adobe Target] Weergaven zijn: we kunnen dit concept benutten in [!DNL Target] om marketers in staat te stellen A/B- en XT-tests uit te voeren op SPA via de VEC. Hiervoor is een eenmalige ontwikkelaarsinstelling vereist. Laten we de stappen doorlopen om dit in te stellen.

1. Installeer om .js 2.*x*.

   Eerst, moeten wij om 2.js installeren.*x*. Deze versie van at.js werd ontwikkeld met SPA in mening. Eerdere versies van at.js bieden geen ondersteuning voor [!DNL Adobe Target] Weergaven en de VEC voor SPA.

   Downloaden om .js 2.*x* via de [!DNL Adobe Target] UI in **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**. te.js 2.*x* kan ook worden geïmplementeerd via tags in [!DNL Adobe Experience Platform].

1. Implementeer het bestand at.js 2.*x* functie, `[triggerView()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)` op uw sites.

   Nadat u de Weergaven van uw SPA hebt gedefinieerd waar u een A/B- of XT-test wilt uitvoeren, implementeert u at.js 2.*x* `triggerView()` gebruiken met Weergaven die als parameter worden doorgegeven. Dit staat marketers toe om VEC te gebruiken om de tests A/B en XT voor die Gedefinieerde Kijken te ontwerpen en in werking te stellen. Als de `triggerView()` De functie wordt niet bepaald voor die Kijken, zal VEC niet de Kijken ontdekken en zo kunnen de verkopers niet VEC gebruiken om A/B en XT tests te ontwerpen en in werking te stellen.

   >[!NOTE]
   >
   >Voor weergaveondersteuning in at.js [viewsEnabled](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#viewsenbabled) moet worden ingesteld op true, anders wordt alle weergavefunctionaliteit uitgeschakeld.

   **`adobe.target.triggerView(viewName, options)`**

   | Parameter | Type | Vereist? | Validatie | Beschrijving |
   | --- | --- | --- | --- | --- |
   | viewName | String | Ja | 1. Geen navolgende spaties.<br />2. Kan niet leeg zijn.<br />3. De weergavenaam moet uniek zijn voor alle pagina&#39;s.<br />4. **Waarschuwing**: De weergavenaam mag niet beginnen of eindigen met &#39;`/`&quot;. De reden hiervoor is dat de klant doorgaans de weergavenaam uit het URL-pad haalt. Voor ons, &quot;home&quot; en &quot;`/home`&quot; verschillen.<br />5. **Waarschuwing**: Dezelfde weergave mag niet meerdere keren achter elkaar worden geactiveerd met de opdracht  `{page: true}` -optie. | Geef een willekeurige naam door als een type tekenreeks dat u de weergave wilt vertegenwoordigen. Deze weergavenaam wordt weergegeven in het dialoogvenster **[!UICONTROL Modifications]** paneel van VEC voor marketers om acties te creëren en hun activiteiten A/B en XT in werking te stellen. |
   | opties | Object | Nee |  |  |
   | opties > pagina | Boolean | Nee |  | **TRUE**: De standaardwaarde van de pagina is true. Wanneer `page=true`, worden meldingen naar Edge-servers verzonden voor een toename van het aantal impressies.<br />**FALSE**: Wanneer `page=false`, worden meldingen niet verzonden voor het verhogen van het aantal impressies. Dit zou moeten worden gebruikt wanneer u een component op een pagina met een aanbieding slechts opnieuw wilt teruggeven. |

   Laten we nu een aantal voorbeelden bekijken van de manier waarop u de `triggerView()` functie in React voor onze hypothetische e-commerce SPA:

   **Koppeling: [Home Site](https://target.enablementadobe.com/react/demo/#/)**

   ![home-response-1](assets/react1.png)

   Als marketers, als wij A/B tests op de volledige homesite willen in werking stellen, dan zouden wij de mening &quot;huis&quot;kunnen willen noemen:

```
 function targetView() {
   var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash

   viewName = viewName || 'home'; // view name cannot be empty

   // Sanitize viewName to get rid of any trailing symbols derived from URL
   if (viewName.startsWith('#') || viewName.startsWith('/')) {
     viewName = viewName.substr(1);
   }

   // Validate if the Target Libraries are available on your website
   if (typeof adobe != 'undefined' && adobe.target && typeof adobe.target.triggerView === 'function') {
     adobe.target.triggerView(viewName);
   }
 }

 // react router v4
 const history = syncHistoryWithStore(createBrowserHistory(), store);
 history.listen(targetView);

 // react router v3
 <Router history={hashHistory} onUpdate={targetView} >
```

**Koppeling: [Productsite](https://target.enablementadobe.com/react/demo/#/products)**

Laten we nu eens kijken naar een voorbeeld dat wat gecompliceerder is. Laten we bijvoorbeeld als marketers de tweede rij van de producten personaliseren door de labelkleur &quot;Prijs&quot; in rood te wijzigen nadat een gebruiker op de knop Meer laden heeft geklikt.

![producten reageren](assets/react4.png)

```
 function targetView(viewName) {
   // Validate if the Target Libraries are available on your website
   if (typeof adobe != 'undefined' && adobe.target && typeof adobe.target.triggerView === 'function') {
     adobe.target.triggerView(viewName);
   }
 }

 class Products extends Component {
   render() {
     return (
       <button type="button" onClick={this.handleLoadMoreClicked}>Load more</button>
     );
   }

   handleLoadMoreClicked() {
     var page = this.state.page + 1; // assuming page number is derived from component's state
     this.setState({page: page});
     targetView('PRODUCTS-PAGE-' + page);
   }
 }
```

**Koppeling: [Afhandeling](https://target.enablementadobe.com/react/demo/#/checkout)**

![uitchecken reageren](assets/react6.png)

Als marketers de inhoud op de site willen aanpassen, afhankelijk van de geselecteerde leveringsvoorkeur, kan een Weergave worden gemaakt voor elke leveringsvoorkeur. In dit geval, wanneer wij Normale Levering selecteren, kan de Mening &quot;Normale Levering worden genoemd.&quot; Als Express Delivery is geselecteerd, kan de weergave de naam &quot;Express Delivery&quot; hebben.

Marketers willen nu een A/B-test uitvoeren om te zien of het wijzigen van de kleur van blauw in rood wanneer de optie Uitdrukkelijke levering is ingeschakeld, conversies kan stimuleren in plaats van de knopkleur blauw te houden voor beide leveringsopties.

```
 function targetView(viewName) {
   // Validate if the Target Libraries are available on your website
   if (typeof adobe != 'undefined' && adobe.target && typeof adobe.target.triggerView === 'function') {
     adobe.target.triggerView(viewName);
   }
 }

 class Checkout extends Component {
   render() {
     return (
       <div onChange={this.onDeliveryPreferenceChanged}>
         <label>
           <input type="radio" id="normal" name="deliveryPreference" value={"Normal Delivery"} defaultChecked={true}/>
           <span> Normal Delivery (7-10 business days)</span>
         </label>

         <label>
           <input type="radio" id="express" name="deliveryPreference" value={"Express Delivery"}/>
           <span> Express Delivery* (2-3 business days)</span>
         </label>
       </div>
     );
   }
   onDeliveryPreferenceChanged(evt) {
     var selectedPreferenceValue = evt.target.value;
     targetView(selectedPreferenceValue);
   }
 }
```

## at.js 2.x systeemdiagrammen

Met de volgende diagrammen krijgt u inzicht in de workflow van at.js 2.x met weergaven en in de manier waarop dit de integratie van SPA verbetert. Voor een betere inleiding van de concepten die in at.js 2.x worden gebruikt, zie [Toepassing van één pagina](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

![Doelstroom met at.js 2.x](../../assets/system-diagram-atjs-20.png)

| Stap | Details |
| --- | --- |
| 1 | De vraag keert identiteitskaart van de Experience Cloud terug als de gebruiker voor authentiek wordt verklaard; een andere vraag synchroniseert de klantenidentiteitskaart. |
| 2 | De bibliotheek at.js wordt synchroon geladen en de hoofdtekst van het document verborgen.<br />at.js kan ook asynchroon worden geladen met een optie die fragment verbergt dat op de pagina is geïmplementeerd. |
| 3 | Er wordt een aanvraag voor het laden van een pagina ingediend, inclusief alle geconfigureerde parameters (MCID, SDID en klant-id). |
| 4 | Profielscripts worden uitgevoerd en vervolgens toegevoegd aan de profielenwinkel. De winkel vraagt om gekwalificeerd publiek uit de Audience Library (bijvoorbeeld publiek dat wordt gedeeld vanuit Adobe Analytics, Publiek beheer, enz.).<br />Klantkenmerken worden in een batchproces naar de profielopslag verzonden. |
| 5 | Gebaseerd op parameters en profielgegevens van het URL-verzoek, [!DNL Target] bepaalt welke activiteiten en ervaringen u wilt retourneren aan de bezoeker voor de huidige pagina en de toekomstige weergaven. |
| 6 | Gerichte inhoud wordt teruggestuurd naar de pagina, waarbij eventueel ook profielwaarden voor extra personalisatie worden opgenomen.<br />Gerichte inhoud op de huidige pagina wordt zo snel mogelijk zichtbaar zonder flikkering van de standaardinhoud.<br />Gerichte inhoud voor weergaven die worden weergegeven als resultaat van gebruikershandelingen in een SPA die in de browser in de cache is opgeslagen, zodat deze direct kan worden toegepast zonder extra serveraanroep wanneer de weergaven worden geactiveerd `triggerView()`. |
| 7 | De analysegegevens worden verzonden naar de servers van de Inzameling van Gegevens. |
| 8 | Gerichte gegevens komen overeen met [!DNL Analytics] gegevens via de SDID en worden verwerkt in de [!DNL Analytics] rapporteringsopslag.<br />De analysegegevens kunnen dan in beide worden bekeken [!DNL Analytics] en [!DNL Target] via [!DNL Analytics] for [!DNL Target] (A4T) verslagen. |

Nu, overal `triggerView()` wordt geïmplementeerd op uw SPA, worden de weergaven en acties opgehaald uit het cachegeheugen en aan de gebruiker getoond zonder een serveraanroep. `triggerView()` verzoekt de Commissie tevens [!DNL Target] achterkant om het aantal beeldingen te verhogen en op te nemen.

![Doelstroom bij.js 2.x triggerView](../../assets/atjs-20-triggerview.png)

| Stap | Details |
| --- | --- |
| 1 | `triggerView()` wordt opgeroepen in de SPA om de weergave te renderen en acties toe te passen om visuele elementen te wijzigen. |
| 2 | De gerichte inhoud voor de mening wordt gelezen van het geheime voorgeheugen. |
| 3 | Gerichte inhoud wordt zo snel mogelijk zichtbaar zonder flikkering van de standaardinhoud. |
| 4 | Aanmelding wordt verzonden naar de [!DNL Target] De Opslag van het profiel om de bezoeker in de activiteit en verhogingsmetriek te tellen. |
| 5 | Analytische gegevens die naar de Servers van de Inzameling van Gegevens worden verzonden. |
| 6 | Doelgegevens komen overeen met [!DNL Analytics] gegevens via de SDID en worden verwerkt in de [!DNL Analytics] rapporteringsopslag. [!DNL Analytics] gegevens kunnen vervolgens in beide worden weergegeven [!DNL Analytics] en [!DNL Target] via A4T-rapporten. |

## Single Page App Visual Experience Composer

Nadat u klaar bent met het installeren van at.js 2.x en het toevoegen `triggerView()` aan uw plaats, gebruik VEC om A/B en XT activiteiten in werking te stellen. Zie voor meer informatie [Single Page App (SPA) Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/spa-visual-experience-composer.html?lang=nl-NL).

>[!NOTE]
>
>De VEC voor SPA is eigenlijk dezelfde VEC als die u gebruikt op gewone webpagina&#39;s, maar er zijn enkele extra mogelijkheden beschikbaar wanneer u een app van één pagina opent met `triggerView()` geïmplementeerd.

## Gebruik TriggerView om ervoor te zorgen dat A4T correct met at.js 2.x en SPA werkt

Om ervoor te zorgen dat [Analyses voor doel](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=nl-NL) (A4T) werkt correct met at.js 2.x, ben zeker om het zelfde SDID in te verzenden [!DNL Target] en in de [!DNL Analytics] verzoek.

Als beste praktijken met betrekking tot SPA:

* Gebruik aangepaste gebeurtenissen om te melden dat er iets interessants in de toepassing gebeurt
* Een aangepaste gebeurtenis activeren voordat de weergave begint met renderen
* Een aangepaste gebeurtenis activeren wanneer de weergave is voltooid

at.js 2.x heeft een nieuwe API toegevoegd [triggerView()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md) functie. U moet `triggerView()` om at.js te laten weten dat een weergave begint met renderen.

Een voorbeeld bekijken om te zien hoe u aangepaste gebeurtenissen, in.js 2.x en Analytics kunt combineren. In dit voorbeeld wordt ervan uitgegaan dat de pagina HTML de API voor bezoekers bevat, gevolgd door at.js 2.x, gevolgd door AppMeasurement.

Laten we aannemen dat de volgende aangepaste gebeurtenissen bestaan:

* `at-view-start` - Wanneer de weergave begint met renderen
* `at-view-end` - Wanneer de weergave is voltooid, wordt rendering voltooid

Om ervoor te zorgen dat A4T met at.js 2.x werkt,

De manager van het meningsbegin zou iets als dit moeten kijken:

```jsx {line-numbers="true"}
document.addEventListener("at-view-start", function(e) {
  var visitor = Visitor.getInstance("<your Adobe Org ID>");
  
  visitor.resetState();
  adobe.target.triggerView("<view name>");
});
```

De manager van het meningseind zou iets als dit moeten kijken:

```jsx {line-numbers="true"}
document.addEventListener("at-view-end", function(e) {
  // s - is the AppMeasurement tracker object
  s.t();
});
```

>[!NOTE]
>
>U moet de `at-view-start` en `at-view-end` gebeurtenissen. Deze gebeurtenissen maken geen deel uit van aangepaste gebeurtenissen at.js.

Hoewel in deze voorbeelden JavaScript-code wordt gebruikt, kan dit alles worden vereenvoudigd als u een tagbeheer gebruikt, zoals tags in [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md).

Als de voorafgaande stappen worden gevolgd zou u een robuuste oplossing A4T voor SPA moeten hebben.

## Best practices implementeren

at.js 2.x APIs laat u uw aanpassen [!DNL Target] de uitvoering is op vele manieren , maar het is belangrijk de juiste volgorde van de werkzaamheden tijdens dit proces te volgen .

De volgende informatie beschrijft de volgorde van bewerkingen die u moet uitvoeren wanneer u voor het eerst een toepassing voor één pagina in een browser laadt en voor elke weergavewijziging die daarna plaatsvindt.

### Volgorde van bewerkingen voor het laden van de eerste pagina {#order}

| Stap | Handeling | Details |
| --- | --- | --- |
| 1 | Bezoeker-API JS laden | Deze bibliotheek is verantwoordelijk voor het toewijzen van een ECID aan de bezoeker. Deze id wordt later gebruikt door andere Adobe-oplossingen op de webpagina. |
| 2 | Laden bij.js 2.x | at.js 2.x laadt alle noodzakelijke APIs die u gebruikt om uit te voeren [!DNL Target] verzoeken en weergaven. |
| 3 | Uitvoeren [!DNL Target] verzoek | Als u een gegevenslaag hebt, adviseren wij dat u kritieke gegevens laadt die worden vereist om naar te verzenden [!DNL Target] voordat de [!DNL Target] verzoek. Dit laat u gebruiken `targetPageParams` om alle gegevens op te nemen die u wilt gebruiken voor het opgeven van doelen.<P>Wanneer `pageLoadEnabled` en `viewsEnabled` zijn ingesteld op true in [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md), in.js vraagt automatisch om alle VEC [!DNL Target] biedt u aan in stap 2.<P>Let op: `getOffers` Kan ook worden gebruikt om VEC-aanbiedingen op te halen nadat de pagina is geladen. Daartoe moet ervoor worden gezorgd dat het verzoek `execute>pageLoad` en `prefetch>views` in de API-aanroep. |
| 4 | Bellen `triggerView()` | Omdat de [!DNL Target] Het verzoek u in Stap 3 in werking stelde kon ervaringen voor zowel de uitvoering van de Lading van de Pagina als Weergaven terugkeren, ervoor zorgen dat `triggerView()` wordt aangeroepen na de [!DNL Target] De aanvraag wordt geretourneerd en het toepassen van de aanbiedingen op cache wordt voltooid. U moet deze stap slechts eenmaal per weergave uitvoeren. |
| 5 | Roep de [!DNL Analytics] paginaweergavebaken | Dit baken verzendt SDID verbonden aan Stap 3 en 4 naar [!DNL Analytics] voor gegevensstitching. |
| 6 | Aanvullende oproep `triggerView({"page": false})` | Dit is een optionele stap voor SPA frameworks die bepaalde componenten op de pagina kunnen renderen zonder dat er een weergavewijziging plaatsvindt. Het is dan ook belangrijk dat u deze API aanroept om ervoor te zorgen dat [!DNL Target] ervaringen worden opnieuw toegepast nadat het SPA framework de componenten opnieuw heeft gerenderd. U kunt deze stap zo vaak uitvoeren als u wilt dat [!DNL Target] de ervaringen blijven in uw SPA. |

### Volgorde van bewerkingen voor SPA wijziging van weergave (geen volledige pagina opnieuw laden)

| Stap | Handeling | Details |
| --- | --- | --- |
| 1 | Bellen `visitor.resetState()` | Deze API zorgt ervoor dat de SDID opnieuw wordt gegenereerd voor de nieuwe weergave terwijl deze wordt geladen. |
| 2 | Cache bijwerken door het `getOffers()` API | Dit is een optionele stap als deze wijziging van de weergave de huidige bezoeker kan kwalificeren voor meer [!DNL Target] activiteiten te verrichten of hen van activiteiten te ontslaan. Op dit punt kunt u ook extra gegevens verzenden naar [!DNL Target] voor het mogelijk maken van verdere doelgerichte capaciteiten. |
| 3 | Bellen `triggerView()` | Als u Stap 2 hebt uitgevoerd, dan moet u op [!DNL Target] vraag en pas de aanbiedingen aan geheime voorgeheugen toe alvorens deze stap uit te voeren. U moet deze stap slechts eenmaal per weergave uitvoeren. |
| 4 | Bellen `triggerView()` | Als u Stap 2 niet hebt uitgevoerd, kunt u deze stap uitvoeren zodra u Stap 1 voltooit. Als u Stap 2 en Stap 3 hebt uitgevoerd, dan zou u deze stap moeten overslaan. U moet deze stap slechts eenmaal per weergave uitvoeren. |
| 5 | Roep de [!DNL Analytics] paginaweergavebaken | Dit baken verzendt SDID verbonden aan Stap 2, 3, en 4 naar [!DNL Analytics] voor gegevensstitching. |
| 6 | Aanvullende oproep `triggerView({"page": false})` | Dit is een optionele stap voor SPA frameworks die bepaalde componenten op de pagina kunnen renderen zonder dat er een weergavewijziging plaatsvindt. Het is dan ook belangrijk dat u deze API aanroept om ervoor te zorgen dat [!DNL Target] ervaringen worden opnieuw toegepast nadat het SPA framework de componenten opnieuw heeft gerenderd. U kunt deze stap zo vaak uitvoeren als u wilt dat [!DNL Target] de ervaringen blijven in uw SPA. |

## Trainingsvideo&#39;s

De volgende video&#39;s bevatten meer informatie:

### Begrijpen hoe at.js 2.x werkt

>[!VIDEO](https://video.tv.adobe.com/v/26250/?quality=12)

Zie [Begrijpen hoe at.js 2.x werkt](https://experienceleague.adobe.com/docs/target-learn/tutorials/implementation/understanding-how-atjs-20-works.html?lang=nl-NL) voor meer informatie .

### Implementeren bij .js 2.x in een SPA

>[!VIDEO](https://video.tv.adobe.com/v/26248/?quality=12)

Zie [Adobe Target- in.js 2.x implementeren in een toepassing voor één pagina (SPA)](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer-for-single-page-applications.html?lang=nl-NL) voor meer informatie .

### VEC gebruiken voor SPA in [!DNL Adobe Target]

>[!VIDEO](https://video.tv.adobe.com/v/26249/?quality=12)

Zie [De Visual Experience Composer gebruiken voor de Toepassing van de Enige Pagina (SPA VEC) in Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer-for-single-page-applications.html?lang=nl-NL) voor meer informatie .
