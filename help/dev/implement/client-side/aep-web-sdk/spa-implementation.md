---
title: De Implementatie van de Toepassing van één pagina voor [!DNL Adobe Experience Platform Web SDK]
description: Leer hoe te om een enig-paginatoepassing (SPA) implementatie van  [!DNL Adobe Experience Platform Web SDK] tot stand te brengen gebruikend  [!DNL Target].
keywords: doel;adobe target;xdm meningen; meningen;enige paginatoepassingen;SPA;SPA levenscyclus;cliënt-kant;AB het testen;AB;Beleving gericht;XT;VEC
feature: AEP Web SDK
source-git-commit: 9a2c35b2d150638fbda00be866f84d2a6faa4300
workflow-type: tm+mt
source-wordcount: '1680'
ht-degree: 0%

---


# Implementatie van één pagina

[!DNL Adobe Experience Platform Web SDK] verstrekt rijke eigenschappen die uw zaken uitrusten om verpersoonlijking op volgende generatie, cliënt-zijtechnologieën zoals single-page toepassingen (SPAs) uit te voeren.

Traditionele websites gebruikten navigatiemodellen &#39;Pagina-naar-pagina&#39;, ook wel &#39;Toepassingen met meerdere pagina&#39;s&#39; genoemd. In deze websites zijn ontwerpen nauw gekoppeld aan URL&#39;s. Voor het schakelen tussen pagina&#39;s is een volledige pagina vereist.

De moderne Webtoepassingen, zoals enig-paginatoepassingen, hebben in plaats daarvan een model aangenomen dat snel gebruik van browser UI teruggeeft, die vaak onafhankelijk van paginaherladingen is. Deze ervaringen worden teweeggebracht door klanteninteractie, zoals scrolls, kliks, en curseurbewegingen. Naarmate de paradigma&#39;s van het moderne web zijn geëvolueerd, werkt de relevantie van traditionele generieke gebeurtenissen, zoals het laden van een pagina, voor het implementeren van personalisatie en experimenten niet meer.

![ Diagram die de levenscyclus van het KUUROORD in vergelijking met traditionele paginaleven tonen.](/help/dev/implement/client-side/aep-web-sdk/assets/spa-vs-traditional-lifecycle.png)

## Voordelen van [!DNL Experience Platform Web SDK] voor SPA&#39;s

Hier volgen enkele voordelen van het gebruik van [!DNL Adobe Experience Platform Web SDK] voor toepassingen die uit één pagina bestaan:

* De capaciteit om alle aanbiedingen op pagina-lading in het voorgeheugen onder te brengen om veelvoudige servervraag aan één enkele servervraag te verminderen.
* Verbeter de gebruikerservaring op uw plaats omdat de aanbiedingen onmiddellijk via het geheime voorgeheugen zonder de vertragingstijd worden getoond die door traditionele servervraag wordt geïntroduceerd.
* Met één coderegel en eenmalige ontwikkelaarsinstelling kunnen marketers [!UICONTROL A/B Test] - en [!UICONTROL Experience Targeting] (XT)-activiteiten maken en uitvoeren via de [!UICONTROL Visual Experience Composer] (VEC) op uw SPA.

## XDM-weergaven en toepassingen van één pagina

[!UICONTROL Adobe Target] VEC voor SPAs haalt voordeel uit een concept genoemd [!UICONTROL Views]: een logische groep visuele elementen die samen een ervaring van het KUUROORD maken. Een toepassing van één pagina kan daarom worden beschouwd als een overgang door meningen, in plaats van URLs, die op gebruikersinteractie wordt gebaseerd. Een [!UICONTROL View] kan doorgaans een hele site of gegroepeerde visuele elementen binnen een site vertegenwoordigen.

In het volgende voorbeeld wordt een hypothetische online e-commercesite gebruikt die in [!DNL React] is geïmplementeerd om voorbeelden [!UICONTROL Views] te verkennen.

Na het navigeren naar de thuissite bevordert een hoofdafbeelding een paasverkoop en de nieuwste producten die op de site beschikbaar zijn. In dit geval kan een [!UICONTROL View] worden gedefinieerd voor het gehele beginscherm. Deze [!UICONTROL View] zou eenvoudig &quot;thuis&quot;kunnen worden genoemd.

![ beeld van de Steekproef van een enig-paginatoepassing in een browser venster.](/help/dev/implement/client-side/aep-web-sdk/assets/example-views.png)

Aangezien de klant meer in de producten geinteresseerd wordt die de zaken verkopen, besluiten zij om de **verbinding van Producten** te klikken. Net als op de thuissite kan de hele productsite worden gedefinieerd als een [!UICONTROL View] . Deze [!UICONTROL View] zou &quot;producten-allen.&quot;kunnen worden genoemd

![ beeld van de Steekproef van een enig-paginatoepassing in browser venster, met alle getoonde producten.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products-all.png)

Omdat een [!UICONTROL View] kan worden gedefinieerd als een hele site of een groep visuele elementen op een site. De vier producten die op de productsite worden weergegeven, kunnen worden gegroepeerd en als een [!UICONTROL View] worden beschouwd. Deze weergave kan &#39;producten&#39; worden genoemd.

![ beeld van de Steekproef van een enig-paginatoepassing in een browser venster, met getoonde voorbeeldproducten.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products.png)

Wanneer de klant besluit om de **Lading Meer** knoop te klikken om meer producten op de plaats te onderzoeken, verandert website URL in dit geval niet. Hier kan echter een [!UICONTROL View] worden gemaakt die alleen de tweede rij producten vertegenwoordigt die wordt weergegeven. De naam van [!UICONTROL View] kan &#39;products-page-2&#39; zijn.

![ beeld van de Steekproef van een enig-paginatoepassing in een browser venster, met voorbeeldproducten die op een extra pagina worden getoond.](/help/dev/implement/client-side/aep-web-sdk/assets/example-load-more.png)

De klant besluit een paar producten van de site te kopen en gaat verder naar het uitcheckscherm. Op de uitchecksite krijgt de klant opties om normale levering of expreslevering te kiezen. Een [!UICONTROL View] kan elke groep visuele elementen op een site zijn. Een [!UICONTROL View] kan dus worden gemaakt voor leveringsvoorkeuren en &quot;Leveringsvoorkeuren&quot; worden genoemd.

![ beeld van de Steekproef van een enig-paginatoepassing controlepagina in een browser venster.](/help/dev/implement/client-side/aep-web-sdk/assets/example-check-out.png)

Het concept van [!UICONTROL Views] kan veel verder worden uitgebreid dan dit scenario. Deze scenario&#39;s zijn slechts een paar voorbeelden van [!UICONTROL Views] die op een site kunnen worden gedefinieerd.

## Implementeren [!UICONTROL XDM Views]

[!UICONTROL XDM Views] kan in [!DNL Target] worden gebruikt om marketers in staat te stellen A/B- en XT-tests uit te voeren op SPA&#39;s via de [!UICONTROL Visual Experience Composer] . Hiervoor moeten de volgende stappen worden uitgevoerd om een eenmalige ontwikkelaarsinstelling te voltooien:

1. Installeer [ SDK van het Web van Adobe Experience Platform ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview).
2. Bepaal alle [!UICONTROL XDM Views] in de toepassing van één pagina die u wilt aanpassen.
3. Nadat u [!UICONTROL XDM Views] hebt gedefinieerd, kunt u voor het uitvoeren van A/B- of XT VEC-activiteiten de functie `sendEvent()` met `renderDecisions` ingesteld op `true` en de bijbehorende [!UICONTROL XDM View] functie in de toepassing Eén pagina implementeren. De [!UICONTROL XDM View] moet worden doorgegeven in `xdm.web.webPageDetails.viewName` . Met deze stap kunnen marketers de [!UICONTROL Visual Experience Composer] gebruiken om A/B- en XT-tests voor deze XDM-tests te starten.

   ```javascript
   alloy("sendEvent", { 
     "renderDecisions": true, 
     "xdm": { 
       "web": { 
         "webPageDetails": { 
         "viewName":"home" 
         }
       } 
     } 
   });
   ```

>[!NOTE]
>
>Bij de eerste `sendEvent()` oproep worden alle [!UICONTROL XDM Views] die aan de eindgebruiker moet worden gerenderd, opgehaald en in cache geplaatst. Volgende `sendEvent()` aanroepen waarvoor [!UICONTROL XDM Views] is doorgegeven, worden gelezen uit de cache en worden zonder een serveraanroep gerenderd.

## `sendEvent()` functievoorbeelden

Deze sectie schetst drie voorbeelden die tonen hoe te om de `sendEvent()` functie in React voor een hypothetische e-commerce SPA aan te halen.

### Voorbeeld 1: Introductiepagina A/B-test

Het marketing team wil tests A/B op de volledige homepage in werking stellen.

![ beeld van de Steekproef van een enig-paginatoepassing in een browser venster.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-1.png)

Als u A/B-tests wilt uitvoeren op de hele thuissite, moet `sendEvent()` worden aangeroepen met de XDM `viewName` ingesteld op `home` :

```jsx
function onViewChange() { 
  
  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash 

  viewName = viewName || 'home'; // view name cannot be empty 

  // Sanitize viewName to get rid of any trailing symbols derived from URL 

  if (viewName.startsWith('#') || viewName.startsWith('/')) { 
    viewName = viewName.substr(1); 
  }
   
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName":"home" 
        } 
      } 
    }
  }); 
} 

// react router v4 

const history = syncHistoryWithStore(createBrowserHistory(), store); 

history.listen(onViewChange); 

// react router v3 

<Router history={hashHistory} onUpdate={onViewChange} > 
```

### Voorbeeld 2: Persoonlijke producten

Het marketing team wil de tweede rij van producten personaliseren door de kleur van het prijsetiket in rood te veranderen nadat een gebruiker **Lading meer** klikt.

![ beeld van de Steekproef van een enig-paginatoepassing in browser venster, tonend gepersonaliseerde aanbiedingen.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-2.png)

```jsx
function onViewChange(viewName) { 

  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName
        }
      } 
    } 
  }); 
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
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### Voorbeeld 3: Voorkeuren voor de aflevering van een A/B-test

Het marketing team wil een test A/B in werking stellen om te zien of veranderend de kleur van de knoop van blauw aan rood wanneer **Uitdrukkelijke Levering** wordt geselecteerd. Het team denkt dat deze verandering omzettingen (in tegenstelling tot het houden van de knoopkleur blauw voor beide leveringsopties) kan verhogen.

![ beeld van de Steekproef van een enig-paginatoepassing in browser venster, met het testen A/B.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-3.png)

Als u de inhoud van de site wilt aanpassen, afhankelijk van de geselecteerde leveringsvoorkeur, kunt u een [!UICONTROL View] maken voor elke leveringsvoorkeur. Wanneer **Normale Levering** wordt geselecteerd, kan [!UICONTROL View] &quot;controle-normaal worden genoemd.&quot; Als **Uitdrukkelijke Levering** wordt geselecteerd, kan [!UICONTROL View] &quot;checkout-express&quot;worden genoemd.

```jsx
function onViewChange(viewName) { 
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName 
        }
      }
    }
  }); 
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
    onViewChange(selectedPreferenceValue); 
  } 

} 
```

## Het gebruiken van [!UICONTROL Visual Experience Composer] voor een SPA

Wanneer u klaar bent met het definiëren van uw [!UICONTROL XDM Views] en `sendEvent()` hebt geïmplementeerd met de [!UICONTROL XDM Views] doorgegeven [!UICONTROL Views] , kan de VEC deze detecteren en kunnen gebruikers handelingen en wijzigingen maken voor A/B- of XT-activiteiten.

>[!NOTE]
>
>Om VEC voor uw KUUROORD te gebruiken, moet u of de [ Uitbreiding van de Helper van Firefox ](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) of [ van Chrome VEC ](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension) installeren en activeren.

### [!UICONTROL Modifications] deelvenster

In het deelvenster [!UICONTROL Modifications] worden de acties vastgelegd die voor een bepaalde [!UICONTROL View] zijn gemaakt. Alle handelingen voor een [!UICONTROL View] worden onder die [!UICONTROL View] gegroepeerd.

### Handelingen

Wanneer u op een handeling klikt, wordt het element op de site gemarkeerd waarop deze handeling wordt toegepast. Elke actie VEC die onder a [!UICONTROL View] wordt gecreeerd heeft de volgende pictogrammen: **Informatie**, **geeft** uit, **Kloon**, **Beweging**, en **schrapt**. Deze pictogrammen worden nader toegelicht in de onderstaande tabel.

| Pictogram | Beschrijving |
|---|---|
| Informatie | Geeft de details van de handeling weer. |
| Bewerken | Hiermee kunt u de eigenschappen van de handeling rechtstreeks bewerken. |
| Klonen | Kloont de handeling naar een of meer [!UICONTROL Views] items in het deelvenster [!UICONTROL Modifications] of naar een of meer [!UICONTROL Views] items in de VEC waarnaar u hebt gebladerd en navigeert. De handeling hoeft niet noodzakelijkerwijs in het deelvenster [!UICONTROL Modifications] te staan.<br/><br/>**Nota:** Nadat een kloonverrichting wordt gemaakt, moet u aan [!UICONTROL View] in VEC via [!UICONTROL Browse] navigeren om te zien of de gekloonde actie een geldige verrichting was. Als de handeling niet op de [!UICONTROL View] kan worden toegepast, wordt er een fout weergegeven. |
| Verplaatsen | Hiermee verplaatst u de handeling naar een [!UICONTROL Page Load Event] of een andere [!UICONTROL View] die al in het deelvenster [!UICONTROL Modifications] bestaat.<br/><br/>**Gebeurtenis van de Lading van de Pagina:** Om het even welke acties die aan de gebeurtenis beantwoorden van de paginading worden toegepast op de aanvankelijke paginading van uw Webtoepassing. <br/><br/>**Nota:** nadat een bewegingsverrichting wordt gemaakt, moet u aan [!UICONTROL View] in VEC via [!UICONTROL Browse] navigeren om te zien of de beweging een geldige verrichting was. Zie een fout als de handeling niet kan worden toegepast op de [!UICONTROL View] . |
| Verwijderen | Hiermee verwijdert u de handeling. |

## Het gebruiken van VEC voor voorbeelden SPAs

Deze sectie schetst drie voorbeelden voor het gebruiken van [!UICONTROL Visual Experience Composer] om acties en wijzigingen voor activiteiten tot stand te brengen A/B of XT.

### Voorbeeld 1: &quot;home&quot;-weergave bijwerken

Eerder in dit artikel is een [!UICONTROL View] met de naam &quot;home&quot; gedefinieerd voor de gehele thuissite. Het marketingteam wil de weergave &quot;home&quot; nu op de volgende manieren bijwerken:

* Verander **toevoegt aan Kar** en **als** knopen aan een lichtere schaduw van blauw. Deze wijziging moet optreden tijdens het laden van de pagina omdat de componenten van de koptekst moeten worden gewijzigd.
* Verander de **Laatste Producten voor 2026** etiket in **HottestProducten voor 2026** en verander de tekstkleur in paars.

Om deze updates in VEC te maken, selecteer **stel** samen en pas die veranderingen op de &quot;huis&quot;mening toe.

![ Visuele de steekproefpagina van de Composer van de Ervaring.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-home.png)

### Voorbeeld 2: productlabels wijzigen

Voor &quot;producten-pagina-2&quot;[!UICONTROL View], zou het marketing team het **Prijs** etiket aan **de Prijs van de Verkoop** willen veranderen en de etiketkleur in rood veranderen.

Om deze updates in VEC te maken, zijn de volgende stappen vereist:

1. Selecteer **doorbladeren** in VEC.
2. Selecteer **Producten** in de hoogste navigatie van de plaats.
3. Selecteer **Lading meer** eens om de tweede rij van producten te bekijken.
4. Selecteer **samenstellen** in VEC.
5. Pas acties toe om het tekstetiket in **de Prijs van de Verkoop** en de kleur aan rood te veranderen.

![ Visuele de steekproefpagina van de Composer van de Ervaring met productetiketten.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-products-page-2.png)

### Voorbeeld 3: Opmaak van leveringsvoorkeuren aanpassen

[!UICONTROL Views] kan worden gedefinieerd op korrelniveau, zoals een status of een optie van een keuzerondje. Eerder in dit artikel werden [!UICONTROL Views] gedefinieerd voor leveringsvoorkeuren, &quot;uitchecken-normaal&quot; en &quot;uitchecken-express&quot;. Het marketingteam wil de kleur van de knop wijzigen in rood voor de weergave &quot;uitchecken-uitdrukken&quot;.

Om deze updates in VEC te maken, zijn de volgende stappen vereist:

1. Selecteer **doorbladeren** in VEC.
2. Voeg op de site producten toe aan het winkelwagentje.
3. Selecteer het winkelwagentje in de rechterbovenhoek van de site.
4. Selecteer **Controle uw Orde**.
5. Selecteer het **Uitdrukkelijke 1} radioknoop van de Levering {** Voorkeur van de Levering **.**
6. Selecteer **samenstellen** in VEC.
7. Verander de **de knoopkleur van het Betalen** in rood.

>[!NOTE]
>
>Het &quot;uitchecken-uitdrukken&quot; [!UICONTROL View] verschijnt niet in het [!UICONTROL Modifications] paneel tot het **Uitdrukkelijke radioknoop van de Levering** wordt geselecteerd. Dit is omdat de `sendEvent()` functie wordt uitgevoerd wanneer het **Uitdrukkelijke 2} radioknoop van de Levering {wordt geselecteerd, daarom is VEC zich niet bewust van &quot;checkout-express&quot;** tot het radioknoop wordt geselecteerd.[!UICONTROL View]

![ Visuele Composer die van de Ervaring leveringsvoorkeur selecteur tonen.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-delivery-preference.png)
