---
keywords: adobe.target.triggerView, triggerView, triggerView, triggerView, at.js, functions, function, viewName, viewname, view name, adobe.target.triggerView1
description: Gebruik de functie adobe.target.triggerView () voor de &lbrace; [!DNL Adobe Target]  at.js JavaScript bibliotheek voor gebruik in de Toepassingen van de Enige Pagina (SPA). (om 2.x.js)
title: Hoe gebruik ik de functie adobe.target.triggerView()?
feature: at.js
exl-id: d6130c56-4e77-4668-ad21-a5b335f8b234
source-git-commit: fe4e607173c760f782035a10f52936d96e9db300
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# adobe.target.triggerView (viewName, options) - at.js 2.x

Deze functie kan worden aangeroepen wanneer een nieuwe pagina wordt geladen of wanneer een component op een pagina opnieuw wordt weergegeven. `adobe.target.triggerView()` moet worden geïmplementeerd voor toepassingen op één pagina (SPA) om [!UICONTROL Visual Experience Composer] (VEC) te gebruiken voor het maken van [!UICONTROL A/B Test] - en [!UICONTROL Experience Targeting] (XT)-activiteiten. Als `[!UICONTROL adobe.target.triggerView()]` niet op de plaats wordt uitgevoerd, kan VEC niet voor SPA worden gebruikt. Voor meer informatie, zie [ Enige implementatie van de Toepassing van de Pagina ](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

>[!NOTE]
>
>Deze functie is geïntroduceerd met at.js 2.*x*. Deze functie is niet beschikbaar voor versie 1 van at.js.*x*.

| Parameter | Type | Vereist? | Beschrijving |
| --- | --- | --- | --- |
| viewName | String | Ja | Geef elke naam door als een type tekenreeks dat u de weergave wilt vertegenwoordigen. Deze weergavenaam wordt in het deelvenster [!UICONTROL Modifications] van de VEC weergegeven, zodat marketers handelingen kunnen maken en hun [!UICONTROL A/B Test] - en [!UICONTROL Experience Targeting] XT-activiteiten kunnen uitvoeren. |
| opties | Object | Nee |  |
| opties > pagina | Boolean | Nee | **WAAR:** De standaardwaarde van pagina is waar. Wanneer page=true, worden meldingen naar de [!DNL Target] backend verzonden voor een toename van het aantal impressies.<P>Er wordt altijd standaard een melding verzonden wanneer een `[!UICONTROL triggerView]` wordt aangeroepen, behalve wanneer opties > pagina is ingesteld op false.<P>**VALS:** Wanneer page=false, worden de berichten niet verzonden voor het verhogen van beeldtelling. Deze benadering zou moeten worden gebruikt wanneer u een component op een pagina met een aanbieding slechts opnieuw wilt teruggeven.<P>**Nota**: De aanbiedingen van de Code van de douane in VEC worden niet opnieuw teruggegeven wanneer `[!UICONTROL triggerView()]` met `{page: false}` als optie wordt geroepen. |

## Voorbeeld: Waar

`[!UICONTROL triggerView()]` -aanroep om een melding naar de [!DNL Target] -backend te verzenden voor het verhogen van activiteitsimpressies en andere metriek.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView")
```

## Voorbeeld: Onwaar

`[!UICONTROL triggerView()]` roept op om geen meldingen naar de [!DNL Target] backend te laten verzenden voor het tellen van de indruk.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView", {page: false})
```

## Voorbeeld: Promise chaining with `getoffers()` and `applyOffers()`

Als u `triggerView()` wilt uitvoeren wanneer de `getOffers()` promise is opgelost, is het belangrijk `triggerView()` uit te voeren op het laatste blok, zoals in het onderstaande voorbeeld wordt getoond. Dit is noodzakelijk voor VEC om `Views` in auteurswijze te ontdekken.

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

## Voorbeeld: De beste compatibiliteit voor `triggerView()` met de [!UICONTROL Adobe Visual Editing Helper extension]

Overweeg het volgende wanneer het gebruiken van de [ Adobe Visuele het Uitgeven uitbreiding van de Helper ](https://experienceleague.adobe.com/nl/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension){target=_blank} :

Vanwege het nieuwe v3 Manifest-beleid van [!DNL Googl] moet de [!UICONTROL Visual Editing Helper extension] op de `DOMContentLoaded` -gebeurtenis wachten voordat de [!DNL Target] -bibliotheken in de VEC worden geladen. [!DNL Chrome] Deze vertraging kan ertoe leiden dat webpagina&#39;s de `triggerView()` -aanroep starten voordat de ontwerpbibliotheken gereed zijn, waardoor de weergave tijdens het laden niet wordt gevuld.

Gebruik een listener voor de gebeurtenis page `load` om dit probleem op te lossen.

Hier volgt een voorbeeldimplementatie:

```javascript
function triggerViewIfLoaded() {
    adobe.target.triggerView("homeView");
}

if (document.readyState === "complete") {
    // If the page is already loaded
    triggerViewIfLoaded();
} else {
    // If the page is not yet loaded, set up an event listener
    window.addEventListener("load", triggerViewIfLoaded);
}
```


