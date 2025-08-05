---
title: Toegang krijgen tot reactietokens met Adobe Experience Platform Web SDK
description: Leer hoe te om tot reactietokens met  [!DNL Adobe Experience Platform Web SDK] toegang te hebben.
keywords: personalisatie;target;adobe target;renderDecisions;sendEvent;decisionsScopes;result.decisions,response tokens;
feature: AEP Web SDK
source-git-commit: f010ca54aac3c2a644a77fb2f88aff1996f6ddfe
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Toegang krijgen tot reactietokens

De inhoud van Personalization die van [!DNL Adobe Target] is teruggekeerd omvat [ reactietokens ](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), die details over de activiteit, de aanbieding, de ervaring, het gebruikersprofiel, geo informatie, en meer zijn. Deze details kunnen met derdehulpmiddelen worden gedeeld of voor het zuiveren worden gebruikt. De tokens van de reactie kunnen in het [!DNL Target] gebruikersinterface worden gevormd.

Om tot om het even welke verpersoonlijkingsinhoud toegang te hebben, verstrek een callback functie wanneer het verzenden van een gebeurtenis. Deze callback wordt geroepen nadat de SDK een succesvolle reactie van de server ontvangt. De callback is voorzien van een `result` -object dat een `propositions` -eigenschap kan bevatten met geretourneerde personalisatie-inhoud. Hieronder ziet u een voorbeeld van een callback-functie.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

In dit voorbeeld is `result.propositions` , indien aanwezig, een array met verpersoonlijkingsvoorstellingen die betrekking hebben op de gebeurtenis. Zie [ teruggevend verpersoonlijkingsinhoud ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content) voor meer informatie over de inhoud van `result.propositions.`

Veronderstel u alle activiteitennamen van alle voorstellen wilt verzamelen die automatisch door het Web SDK werden teruggegeven en hen duwen in één enkele serie. Vervolgens kunt u de ene array naar een derde verzenden. In dit geval:

1. Extraheer voorstellen uit het `result` -object.
1. Lijn door elk voorstel.
1. Bepaal of de SDK het voorstel heeft weergegeven.
1. Als zo, lijn door elk punt in het voorstel.
1. Haal de naam van de activiteit op uit de eigenschap `meta` . Dit is een object dat responstokens bevat.
1. Zet de naam van de activiteit in een array.
1. Verzend de namen van de activiteiten naar een derde.

Uw code ziet er als volgt uit:

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    var activityNames = [];
    propositions.forEach(function(proposition) {
      if (proposition.renderAttempted) {
        proposition.items.forEach(function(item) {
          if (item.meta) {
            // item.meta contains the response tokens.
            var activityName = item.meta["activity.name"];
            // Ignore duplicates
            if (activityNames.indexOf(activityName) === -1) {
              activityNames.push(activityName);
            }
          }
        });
      }
    });
    // Now that activity names are in an array,
    // you can send them to a third party or use
    // them in some other way.
  });
```
