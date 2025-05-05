---
keywords: adobe.target.trackEvent, trackEvent, trackevent, track event, at.js, functions, function, preventDefault, preventdefault, prevent default, adobe.target.trackEvent
description: Gebruik de [!UICONTROL adobe.target.trackEvent()] functie voor de [!DNL Adobe Target] om.js JavaScript bibliotheek in werking te stellen om een verzoek in werking te stellen om gebruikersacties, zoals kliks en omzettingen op uw plaats te melden.
title: Hoe gebruik ik de [!UICONTROL adobe.target.trackEvent()] Functie?
feature: at.js
exl-id: 9a55e4f1-d7f9-47c1-867c-2ce06fb26f9f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# [!UICONTROL adobe.target.trackEvent(options)]

Deze functie voert een verzoek in om gebruikersacties, zoals kliks en omzettingen te melden. Het levert geen activiteiten in de reactie.

Deze gebeurtenis-volgende mbox vraag kan dan worden gebruikt om metriek in activiteiten te bepalen. Zie voor meer informatie [Succeswaarden](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=nl-NL) en [Conversies bijhouden](../how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions).

Hier volgen de API-details:

| Sleutel | Type | Vereist | Beschrijving |
|--- |--- |--- |--- |
| mbox | String | Ja | Naam van vak<P>**Opmerking**: Als een [!UICONTROL trackEvent()] de vraag wordt in brand gestoken met een mbox naam die reeds op de pagina, SDID van [!UICONTROL trackEvent()] wordt opnieuw ingesteld en zal anders zijn dan de [!DNL Target] roept op de pagina. Het afvuren van [!UICONTROL trackEvent()] de vraag met een verschillende naam van de doos houdt [!UICONTROL trackEvent()] SDID van de vraag verenigbaar met [!UICONTROL Page Load Request]/[!UICONTROL triggerView()] roept op de pagina. |
| kiezer | String | Nee | CSS-kiezers die worden gebruikt om de HTML-elementen te zoeken. De gebeurtenislisteners worden aan gevonden elementen gekoppeld. |
| type | String | Nee | Vertegenwoordigt een geregistreerd gebeurtenistype. Dit kunnen HTML bekende gebeurtenissen zijn, zoals: klikken, mousedown, enzovoort, en aangepaste HTML-gebeurtenissen. |
| preventDefault | Boolean | Nee | Geeft aan of u wilt gebruiken `[!UICONTROL event.preventDefault()]` in de gebeurtenislistener-callback. De standaardwaarde is false.<P>**Opmerking** Alleen : `[!UICONTROL form[submit]]` en `a[click]` worden ondersteund. Andere scenario&#39;s worden niet gesteund wegens ingewikkeldheid en enorme hoeveelheid te steunen scenario&#39;s. |
| param | Object | Nee | Mbox-parameters. Een object van sleutelwaardeparen met de volgende structuur:<P>`{ "param1": "value1", "param2": "value2"}` |
| timeout | Getal | Nee | Time-out in milliseconden.<P>Indien niet opgegeven, wordt de standaardwaarde gebruikt:<P>`...timeoutInSeconds: 0.15...}` |
| succes | -functie | Nee | Een callback-functie die wordt gebruikt om aan te geven dat de gebeurtenis is gerapporteerd. |
| fout | -functie | Nee | Een callback-functie die wordt gebruikt om aan te geven dat de gebeurtenis niet kon worden gerapporteerd. |

## Voorbeeld

```javascript {line-numbers="true"}
<a href="https://asite.com">click me!</a> 
```

plus JavaScript-code die moet worden toegewezen `trackEvent`:

```javascript {line-numbers="true"}
<script> 
$('a').click(function(event){ 
  adobe.target.trackEvent({'mbox':'homePageHero'}) 
}); 
</script> 
```

Of:

```javascript {line-numbers="true"}
adobe.target.trackEvent({ 
    "mbox": "clicked-cta", 
    "params": { 
        "param1": "value1" 
    } 
});
```

>[!WARNING]
>
>Als de verplichte velden niet zijn ingesteld, wordt geen aanvraag uitgevoerd en wordt een fout gegenereerd.
