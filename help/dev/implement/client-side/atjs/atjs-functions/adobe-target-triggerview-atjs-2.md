---
keywords: adobe.target.triggerView, triggerView, triggerView, triggerView, at.js, functions, function, viewName, viewname, view name, adobe.target.triggerView1
description: Gebruik de functie adobe.target.triggerView() voor de [!DNL Adobe Target] at.js JavaScript-bibliotheek voor gebruik in toepassingen voor één pagina (SPA). (om 2.x.js)
title: Hoe gebruik ik de functie adobe.target.triggerView()?
feature: at.js
exl-id: d6130c56-4e77-4668-ad21-a5b335f8b234
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# adobe.target.triggerView (viewName, options) - at.js 2.x

Deze functie kan worden aangeroepen wanneer een nieuwe pagina wordt geladen of wanneer een component op een pagina opnieuw wordt weergegeven. `adobe.target.triggerView()` moet worden geïmplementeerd voor toepassingen van één pagina (SPA) om de [!UICONTROL Visual Experience Composer] (VEC) om [!UICONTROL A/B Test] en [!UICONTROL Experience Targeting] (XT) activiteiten. Indien `[!UICONTROL adobe.target.triggerView()]` niet op het terrein wordt geïmplementeerd, kan de VEC niet voor SPA worden gebruikt. Zie voor meer informatie [Toepassing van één pagina](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

>[!NOTE]
>
>Deze functie is geïntroduceerd met at.js 2.*x*. Deze functie is niet beschikbaar voor versie 1 van at.js.*x*.

| Parameter | Type | Vereist? | Beschrijving |
| --- | --- | --- | --- |
| viewName | String | Ja | Geef elke naam door als een type tekenreeks dat u de weergave wilt vertegenwoordigen. Deze weergavenaam wordt weergegeven in het dialoogvenster [!UICONTROL Modifications] deelvenster VEC voor marketers om handelingen te maken en hun [!UICONTROL A/B Test] en [!UICONTROL Experience Targeting] XT-activiteiten. |
| opties | Object | Nee |  |
| opties > pagina | Boolean | Nee | **TRUE:** De standaardwaarde van de pagina is true. Als page=true is, worden meldingen verzonden naar de [!DNL Target] voor het verhogen van het aantal imkers.<P>Een bericht wordt altijd standaard verzonden wanneer een `[!UICONTROL triggerView]` wordt aangeroepen, behalve wanneer opties > pagina is ingesteld op false.<P>**FALSE:** Wanneer page=false, worden geen meldingen verzonden voor het verhogen van het aantal impressies. Deze benadering zou moeten worden gebruikt wanneer u een component op een pagina met een aanbieding slechts opnieuw wilt teruggeven.<P>**Opmerking**: Aanbiedingen voor aangepaste code in de VEC worden niet opnieuw weergegeven wanneer `[!UICONTROL triggerView()]` wordt aangeroepen met `{page: false}` als de optie. |

## Voorbeeld: Waar

`[!UICONTROL triggerView()]` oproep om een bericht naar de [!DNL Target] back-end voor het verhogen van activiteitsimpressies en andere metriek.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView")
```

## Voorbeeld: Onwaar

`[!UICONTROL triggerView()]` oproep om geen meldingen naar de [!DNL Target] voor het tellen van de indruk.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView", {page: false})
```

## Voorbeeld: beloften koppelen met `getoffers()` en `applyOffers()`

Uitvoeren `triggerView()` wanneer de `getOffers()` belofte is opgelost, het is belangrijk om uit te voeren `triggerView()` op het laatste blok, zoals in het onderstaande voorbeeld wordt getoond. Dit is nodig voor de VEC om `Views` in de ontwerpmodus.

```javascript {line-numbers="true"}
adobe.target.getOffers({
    'request': {
        'prefetch': {
            'views': [{
                'parameters': {}
            }]
        }
    }
}).then(function(response) {
    // Apply Offers
    adobe.target.applyOffers({
        response: response
    });
}).catch(function(error) {
    console.log("AT: getOffers failed - Error", error);
}).finally(() => {
    // Trigger View call, assuming pageView is defined elsewhere
    adobe.target.triggerView(pageView, {
        page: true
    });
    console.log('AT: View triggered on : ' + pageView);
});
```
