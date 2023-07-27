---
keywords: adobe.target.applyOffers, applyOffers, apply aanbiedingen, apply aanbiedingen, at.js, functions, function,
description: Gebruik de [!UICONTROL adobe.target.applyOffers()] functie voor de [!DNL Adobe Target] JavaScript-bibliotheek at.js om meerdere aanbiedingen in de reactie toe te passen. (om 2.x.js)
title: Hoe gebruik ik de [!UICONTROL adobe.target.applyOffers()] Functie?
feature: at.js
exl-id: c391e3f4-fdf1-4e33-8dcb-6bf46e390538
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---

# [!UICONTROL adobe.target.applyOffers(options)] - om.js 2.x

Met deze functie kunt u meerdere aanbiedingen toepassen die zijn opgehaald door `adobe.target.getOffers()`.

>[!NOTE]
>
>Deze functie is geïntroduceerd met at.js 2.*x*. Deze functie is niet beschikbaar voor versie 1 van at.js.*x*.

| Sleutel | Type | Vereist? | Beschrijving |
| --- | --- | --- | --- |
| kiezer | String | Nee | HTML-element of CSS-kiezer die wordt gebruikt om het HTML-element te identificeren waar [!DNL Target] moet de inhoud van het voorstel plaatsen. Als er geen kiezer is, [!DNL Target] gaat ervan uit dat het HTML-element dat moet worden gebruikt HTML HEAD is. |
| Antwoord | Object | Ja | Object Response van `getOffers()`.<br />Zie onderstaande tabel Verzoeken. |

## Antwoord

>[!NOTE]
>
>Raadpleeg de [Leverings-API-documentatie](/help/dev/implement/delivery-api/overview.md) voor informatie over de acceptabele typen voor alle onderstaande velden.

| Veldnaam | Beschrijving |
| --- | --- |
| response > prefetch > views > options > content | De inhoud van de optie &quot;option&quot; is niet goed gedefinieerd en hangt rechtstreeks af van het optietype/de sjabloonstructuur. |
| response > prefetch > views > options > type | Type optie. Geeft het type &quot;content&quot;-veld aan. Ondersteund type is handelingen. |
| response > prefetch > views > state | Een ondoorzichtig token voor weergavestatus dat moet worden doorgestuurd met een weergavemelding voor de weergave |
| response > prefetch > views > options > responseTokens | Bevat de kaart van `responseTokens` die zijn verzameld bij de verwerking van de huidige optie. |
| response > prefetch > views > analytics > payload | [!DNL Analytics] payload voor integratie op de client die moet worden verzonden naar [!DNL Analytics] nadat de weergave is toegepast. |
| response > prefetch > views > trace | Het object met alle traceergegevens voor de aanroep van de prefetch per weergave.<br />Het spoorvoorwerp zal ook een versie voor het spoor omvatten.<br />Het spoorvoorwerp zal ook details van de huidige mening omvatten. |
| response > prefetch > views > options > eventToken | Gebeurtenislogbestanden worden per optie uitgevoerd. Voor elke toegepaste optie moet de respectievelijke gebeurtenistoken worden toegevoegd aan de lijst met meldingstokens. Een weergave bestaat uit meerdere opties. Als alle opties zijn toegepast en weergegeven, alle `eventTokens` in de kennisgeving moeten worden opgenomen. |
| response > prefetch > views > name | De voor mensen leesbare weergavenaam. |
| response > prefetch > views > metrics | Metriek melden die zou moeten worden gecontroleerd en dan op de hoogte brengen [!DNL Target] ongeveer. Momenteel wordt alleen het klikken op metrisch ondersteund. Als er op het element wordt geklikt, wordt het juiste `eventTokens` moeten worden verzameld en moet een kennisgeving worden gezonden. |
| response > prefetch > views > key | De sleutel of vingerafdruk die de weergave identificeert. |
| response > prefetch > views > id | Id van de weergave. |
| response > notifications > id | Berichtings-id. |
| reactie > meldingen > gebeurtenissen > type | Het type van het bericht, klik, of vertoning. |
| reactie > meldingen > gebeurtenissen > trace | Het spoor voor de berichtgebeurtenis. |
| reactie > meldingen > gebeurtenissen > token | Het token dat met de meldingsgebeurtenis is verzonden. |
| response > notifications > events > timestamp | De tijdstempel die met de meldingsgebeurtenis is verzonden. |
| response > notifications > events > errorCode | Als de melding is mislukt, geeft de code de oorzaak van de fout aan. |
| response > notifications > events | De gebeurtenissen die werden geregistreerd of er niet in geslaagd om voor het huidige bericht worden geregistreerd. |
| response > notifications | Geeft de geregistreerde of mislukte meldingen aan. |
| response > execute > boxes > mbox > trace | Het object met alle traceergegevens voor de afzonderlijke mbox-aanvraag. |
| response > execute > mboxes > mbox > responseTokens | Bevat kaart van `responseTokens` voor specifieke mbox verzoek uitvoeren. |
| response > execute > boxes > mbox > option > content | De inhoud van de optie &quot;option&quot; is niet goed gedefinieerd en hangt rechtstreeks af van het optietype/de sjabloonstructuur. |
| response > execute > boxes > mbox > option > type | Type optie. Geeft het type &quot;content&quot;-veld aan. Ondersteunde typen zijn: html, redirect, JSON en dynamic. |
| response > execute > boxes > mbox > options | Reactieoptie. |
| response > execute > mboxes > metrics > eventToken | Token van gebeurtenis click. |
| response > execute > boxes > mbox > metrics > type | &quot;click&quot; |
| response > execute > boxes > mbox > metrics | Bevat lijst met `clickThrough` metriek. |
| response > execute > boxes > mbox > mbox | De naam van de mbox. |
| response > execute > boxes > mbox >index | Geeft aan dat de reactie wordt gegeven voor mbox met deze index van de aanvraag. |
| response > execute > mboxen > mbox > analytics > payload | [!DNL Analytics] payload voor integratie op de client die moet worden verzonden naar [!DNL Analytics] nadat het mbox is toegepast. (Zie de sectie Campagnes die geschikt zijn voor A4T.) |
| response > execute > boxes | Lijst met uitvoerbare vakken. |
| response > execute > pageLoad > options > content | De inhoud van de optie &quot;option&quot; is niet goed gedefinieerd en hangt rechtstreeks af van het optietype/de sjabloonstructuur. |
| response > execute > pageLoad > options > type | Type optie. Geeft het type &quot;content&quot;-veld aan. Ondersteunde typen zijn: html, redirect, JSON, dynamic en actions. |
| response > execute > pageLoad > options | Opties die niet door meningen (doel-globaal-mbox + opties van activiteiten met meningen worden gegroepeerd die niet door meningen) worden gegroepeerd. |
| response > execute > pageLoad > metrics | Klik op Metriek die niet is ingesteld om tot een bepaalde weergave te behoren. |
| response > execute > pageLoad > trace | Het object met alle traceergegevens voor de pageLoad-aanvraag. |
| response > execute > pageLoad > analytics > payload | [!DNL Analytics] payload voor integratie op de client die moet worden verzonden naar [!DNL Analytics] nadat de pagina inhoud heeft geladen. (Zie de sectie Campagnes die geschikt zijn voor A4T.) |

## Voorbeeld [!UICONTROL applyOffers()] call

```javascript {line-numbers="true"}
adobe.target.applyOffers({response:{
  "execute": {
    "pageLoad": {
      "options": [{
        "type": "html",
        "content": "page-load"
      },
      {
        "type": "actions",
        "content": [{
          "type": "setHtml",
          "content": "<h1>Container 1</h1>",
          "selector": "#container1",
          "cssSelector": "#container1"
        },
        {
          "type": "setHtml",
          "content": "<h3>Container 3</h3>",
          "selector": "#container3",
          "cssSelector": "#container3"
        }]
      }],
 
 
      "metrics": [{
        "type": "click",
        "selector": "#container1",
        "eventToken": "page-load-click-metric" 
      }]
    }
  }
}});
```

## Voorbeelden van aanroepen van Promise-ketting met `[!UICONTROL getOffers()]` en `[!UICONTROL applyOffers()]`, omdat deze functies zijn gebaseerd op Promise

```javascript {line-numbers="true"}
adobe.target.getOffers({...})
.then(response => adobe.target.applyOffers({ response: response }))
.then(() => console.log("Success"))
.catch(error => console.log("Error", error));
```

Raadpleeg de getOffers voor meer voorbeelden over het gebruik van getOffers() [documentatie](adobe-target-getoffers-atjs-2.md)

### Voorbeeld van aanvraag voor laden van pagina


```javascript {line-numbers="true"}
adobe.target.getOffers({
    request: {
        execute: {
            pageLoad: {}
        }
    }
}).
then(response => adobe.target.applyOffers({ response: response }))
.then(() => console.log("Success"))
.catch(error => console.log("Error", error));
```
