---
title: Bij.js vergelijken met de Experience Platform Web SDK
description: Leer hoe de at.js eigenschappen met  [!DNL Experience Platform Web SDK] vergelijken.
keywords: doel;adobe target;activity.id;experience.id;renderDecisions;DecisionScopes;prehide snippet;vec;Form-Based Experience Composer;xdm;publiek;decisions;scope;schema;system diagram;diagram
feature: AEP Web SDK
source-git-commit: d6b93537692a1efbc2650a015f5a44d4fd1fd422
workflow-type: tm+mt
source-wordcount: '2006'
ht-degree: 0%

---

# De bibliotheek at.js vergelijken met de [!DNL Adobe Experience Platform Web SDK]

## Overzicht

Dit artikel biedt een overzicht van de verschillen tussen de `at.js` -bibliotheek en de Experience Platform Web SDK.

## Bibliotheken installeren

### Installeer at.js

Met [!DNL Adobe] kunnen klanten de bibliotheek rechtstreeks downloaden vanaf het tabblad [!DNL Adobe Experience Cloud] , [!UICONTROL Implementation] . De bibliotheek at.js wordt aangepast met instellingen die de klant als volgt heeft: clientCode, imsOrgId, enz.

### De Web SDK installeren

De vooraf gebouwde versie is beschikbaar op een CDN. U kunt de bibliotheek op CDN rechtstreeks op uw pagina van verwijzingen voorzien, of het downloaden en ontvangen op uw eigen infrastructuur. Het is beschikbaar in geminiatuurde en ongeminificeerde formaten. De ongeminificeerde versie is handig voor foutopsporingsdoeleinden.

Zie [ SDK van het Web installeren gebruikend de bibliotheek van JavaScript ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/library) voor meer informatie.

## De bibliotheken configureren

### Bij.js configureren

Aan het einde van elk bestand at.js ziet u een sectie waarin [!DNL Adobe] een instellingsobject instantieert en doorgeeft. Deze kan worden aangepast wanneer Adobe het desbetreffende gedeelte downloadt en de huidige instellingen van de klant erin opneemt.

```javascript
window.adobe.target.init(window, document, {
  "clientCode": "demo",
  "imsOrgId": "",
  "serverDomain": "localhost:5000",
  "timeout": 2000,
  "globalMboxName": "target-global-mbox",
  "version": "2.0.0",
  "defaultContentHiddenStyle": "visibility: hidden;",
  "defaultContentVisibleStyle": "visibility: visible;",
  "bodyHiddenStyle": "body {opacity: 0 !important}",
  "bodyHidingEnabled": true,
  "deviceIdLifetime": 63244800000,
  "sessionIdLifetime": 1860000,
  "selectorsPollingTimeout": 5000,
  "visitorApiTimeout": 2000,
  "overrideMboxEdgeServer": false,
  "overrideMboxEdgeServerTimeout": 1860000,
  "optoutEnabled": false,
  "optinEnabled": false,
  "secureOnly": false,
  "supplementalDataIdParamTimeout": 30,
  "authoringScriptUrl": "//cdn.tt.omtrdc.net/cdn/target-vec.js",
  "urlSizeLimit": 2048,
  "endpoint": "/rest/v1/delivery",
  "pageLoadEnabled": true,
  "viewsEnabled": true,
  "analyticsLogging": "server_side",
  "serverState": {},
  "decisioningMethod": "server-side",
  "legacyBrowserSupport":  false
});
```

[Meer informatie](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)

### De Platform Web SDK configureren

De configuratie voor SDK wordt gedaan met het [`configure` ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/overview) bevel. Het `configure` bevel is altijd ** geroepen eerst.

## Aanbiedingen voor het aanvragen en automatisch renderen van het laden van pagina&#39;s [!DNL Target]

### At.js gebruiken

Als u de instelling `pageLoadEnabled,` inschakelt, activeert de bibliotheek met behulp van at.js 2.x een aanroep van [!DNL Target] Edge met `execute -> pageLoad` . Als alle instellingen op de standaardwaarden zijn ingesteld, is aangepaste codering niet nodig. Zodra om.js aan de pagina wordt toegevoegd en door browser wordt geladen, wordt een [!DNL Target] vraag van Edge uitgevoerd.

### [!DNL PLatform Web SDK] gebruiken

De inhoud die binnen [!DNL Target] [ wordt gecreeerd Visuele Composer van de Ervaring ](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/visual-experience-composer) kan automatisch door SDK worden teruggewonnen en worden teruggegeven.

Als u [!DNL Target] -aanbiedingen wilt aanvragen en automatisch wilt renderen, gebruikt u de opdracht `sendEvent` en stelt u de optie `renderDecisions` in op `true.` Zo dwingt u de SDK om automatisch gepersonaliseerde inhoud te renderen die in aanmerking komt voor automatische rendering.

Voorbeeld:

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

[!DNL Experience Platform Web SDK] verzendt automatisch een melding met de aanbiedingen die door [!DNL Platform WEB SDK] werden uitgevoerd. Dit is een voorbeeld van hoe een lading van het berichtverzoek als kijkt:

```json
{
  "events": [{
      "xdm": {
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                "scope": "cart",
                "scopeDetails": {
                  "decisionProvider": "TGT",
                  "activity": {
                    "id": "127019"
                  },
                  "experience": {
                    "id": "0"
                  },
                  "strategies": [
                    {
                      "step": "entry",
                      "algorithmID": "0",
                      "trafficType": "0"
                    },
                    {
                      "step": "display",
                      "algorithmID": "0",
                      "trafficType": "0"
                    }
                  ],
                  "characteristics": {
                    "eventToken": "bKMxJ8dCR1XlPfDCx+2vSGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                  }
                }
              }
            ]
          }
        },
        "eventType": "display",
        "web": {
          "webPageDetails": {
            "viewName": "cart",
            "URL": "https://alloyio.com/personalizationSpa/cart"
          },
          "webReferrer": {
            "URL": ""
          }
        },
        "device": {
          "screenHeight": 800,
          "screenWidth": 1280,
          "screenOrientation": "landscape"
        },
        "environment": {
          "type": "browser",
          "browserDetails": {
            "viewportWidth": 1280,
            "viewportHeight": 284
          }
        },
        "placeContext": {
          "localTime": "2021-12-10T15:50:34.467+02:00",
          "localTimezoneOffset": -120
        },
        "timestamp": "2021-12-10T13:50:34.467Z",
        "implementationDetails": {
          "name": "https://ns.adobe.com/experience/alloy",
          "version": "2.6.2",
          "environment": "browser"
        }
      }
    }
  ]
}
```

[ Leer meer ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## Hoe te om te verzoeken en *NIET* automatisch de aanbiedingen van het Doel van de Lading van de Pagina terug te geven

### At.js gebruiken

Er zijn twee manieren om een aanroep van [!DNL Target] Edge te activeren die aanbiedingen voor het laden van pagina&#39;s ophaalt.

Voorbeeld 1:

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox", 
   success: console.log,
   error: console.error
});
```

Voorbeeld 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

[ Leer meer ](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/atjs-functions)

### [!DNL Platform Web SDK] gebruiken

Voer een opdracht `sendEvent` uit met een speciaal bereik onder `decisionScopes` : `__view__` . [!DNL Adobe] gebruikt dit bereik als een signaal om alle activiteiten voor het laden van pagina&#39;s op te halen uit [!DNL Target] en alle weergaven vooraf in te stellen. [!DNL Platform Web SDK] probeert ook om alle VEC mening gebaseerde activiteiten te evalueren. Het uitschakelen van weergave-prefetching wordt momenteel niet ondersteund in de [!DNL Platform Web SDK] .

Om tot om het even welke verpersoonlijkingsinhoud toegang te hebben, kon u een callback functie verstrekken, die zal worden geroepen nadat SDK een succesvolle reactie van de server ontvangt. Uw callback wordt verstrekt een resultaatvoorwerp, dat voorzetbezit zou kunnen bevatten die om het even welke teruggekeerde verpersoonlijkingsinhoud bevatten.

Voorbeeld:

```javascript
alloy("sendEvent", {
    xdm: {...},
    decisionScopes: ["__view__"]
  }).then(function(result) {
    if (result.propositions) {
      result.propositions.forEach(proposition => {
        proposition.items.forEach(item => {
          if (item.schema === HTML_SCHEMA) {
            // manually apply offer
            document.getElementById("form-based-offer-container").innerHTML =
              item.data.content;
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
          // manually send the display notification event, so that Target/Analytics impressions aare increased
            alloy("sendEvent",{
              "xdm": {
                "eventType": "decisioning.propositionDisplay",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          }
        });
      });
    }
  });
```

[ Leer meer ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## Specifieke doelvakken voor formulieren aanvragen

### At.js gebruiken

U kunt activiteiten ophalen met de functie `getOffer` :

Voorbeeld 1:

```javascript
adobe.target.getOffer({
   mbox: "hero-banner", 
   success: console.log,
   error: console.error
});
```

Voorbeeld 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        mboxes: [
        {
          index: 0,
          name: "hero-banner"
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

[ Leer meer ](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/atjs-functions.html)

### [!DNL Platform Web SDK] gebruiken

U kunt op [!UICONTROL Form-Based Composer] gebaseerde activiteiten ophalen door de opdracht `sendEvent` te gebruiken en de namen van de box onder de optie `decisionScopes` door te geven. De opdracht `sendEvent` retourneert een belofte die wordt opgelost met een object dat de gevraagde activiteiten/voorstellen bevat:

Met dit codefragment ziet de array `propositions` er als volgt uit:

```javascript
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg=="
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

Voorbeeld:

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];
        if (item.schema === HTML_SCHEMA) {
          // apply offer
          document.getElementById("form-based-offer-container").innerHTML =
            item.data.content;
          const executedPropositions = [
            {
              id: proposition.id,
              scope: proposition.scope,
              scopeDetails: proposition.scopeDetails
            }
          ];

          alloy("sendEvent", {
            "xdm": {
              "eventType": "decisioning.propositionDisplay",
              "_experience": {
                "decisioning": {
                  "propositions": executedPropositions
                }
              }
            }
          });
        }
      }
    }
  }
});
```

[ Leer meer ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## De [!DNL Target] -activiteiten toepassen

### At.js gebruiken

U kunt de [!DNL Target] -activiteiten toepassen met de functie `applyOffers` : `adobe.target.applyOffer(options).`

Voorbeeld:

```javascript
adobe.target.getOffers({...})
  .then(response => adobe.target.applyOffers({ response: response }))
  .then(() => console.log("Success"))
  .catch(error => console.log("Error", error));
```

Leer meer over het `applyOffers` bevel van de [ specifieke documentatie ](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/adobe-target-applyoffers-atjs-2).

### [!DNL Platform Web SDK] gebruiken

U kunt de [!DNL Target] -activiteiten toepassen met de opdracht `applyPropositions` .

Voorbeeld:

```javascript
alloy("applyPropositions", {
    propositions: [...]
});
```

Leer meer over het `applyPropositions` bevel van de [ specifieke documentatie ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content).

## Hoe kan ik gebeurtenissen volgen?

### At.js gebruiken

U kunt gebeurtenissen volgen met de functie `trackEvent` of met `sendNotifications.`

Deze functie voert een verzoek in om gebruikersacties, zoals kliks en omzettingen te melden. Deze functie levert geen activiteiten in de reactie.

**Voorbeeld 1**

```javascript
adobe.target.trackEvent({ 
    "type": "click",
    "mbox": "some-mbox"
});
```

**Voorbeeld 2**

```javascript
adobe.target.sendNotifications({ 
    request: {
       notifications: [{
          ...,
          mbox: {
            name: "some-mbox"
          },
          type: "click",
          ...
       }]
    }
});
```

[ Leer meer ](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-trackevent.html)

### [!DNL Platform Web SDK] gebruiken

U kunt gebeurtenissen en gebruikersacties volgen door de opdracht `sendEvent` aan te roepen, de `_experience.decisioning.propositions` XDM `fieldgroup` te vullen en de `eventType` op een van twee waarden in te stellen:

* `decisioning.propositionDisplay`: hiermee wordt het renderen van de [!DNL Target] -activiteit aangegeven.
* `decisioning.propositionInteract`: hiermee wordt een gebruikersinteractie met de activiteit aangegeven, zoals een muisklik.

`_experience.decisioning.propositions` XDM `fieldgroup` is een array met objecten. De eigenschappen van elk object worden afgeleid van de `result.propositions` die wordt geretourneerd in de `sendEvent` command: `{ id, scope, scopeDetails }.`

**Voorbeeld 1 - spoor a `decisioning.propositionDisplay` gebeurtenis na het teruggeven van een activiteit**

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['discount']
}).then(function(result) {
  var propositions = result.propositions;

  var discountProposition;
  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      if (proposition.scope === "discount") {
        discountProposition = proposition;
        break;
      }
    }
  }

  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        var discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
        break;  
      }
    }
    // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered.
    alloy("sendEvent", {
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": [{
              "id": id,
              "scope": scope,
              "scopeDetails": scopeDetails
            }],
            "propositionEventType": {
              "display": 1
            }
          }
        }
      }
    });
  }
});
```

**Voorbeeld 2 - Spoor a `decisioning.propositionInteract` gebeurtenis na klikken metrisch voorkomt**

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items.length; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

[ Leer meer ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content#manual)

**Voorbeeld 3 - spoor een gebeurtenis die na het uitvoeren van een actie** wordt ontbrand

In dit voorbeeld wordt een gebeurtenis bijgehouden die is geactiveerd nadat een bepaalde handeling is uitgevoerd, zoals het klikken op een knop.
U kunt aanvullende aangepaste parameters toevoegen via het gegevensobject `__adobe.target` .

U kunt ook het `commerce` XDM-object toevoegen.

```js
alloy("sendEvent", {
    "xdm": {
        "_experience": {
            "decisioning": {
                "propositions": [
                    {
                        "scope": "orderConfirm" //example scope name
                    }
                ],
                "propositionEventType": {
                    "display": 1
                }
            }
        },
        "eventType": "decisioning.propositionDisplay"
    },
    "commerce": {
        "order": {
            "purchaseID": "a8g784hjq1mnp3",
            "purchaseOrderNumber": "VAU3123",
            "currencyCode": "USD",
            "priceTotal": 999.98
        }
    },
    "data": {
        "__adobe": {
            "target": {
                "pageType": "Order Confirmation",
                "user.categoryId": "Insurance"
            }
        }
    }
})
```

## Een weergavewijziging activeren in een toepassing voor één pagina

### At.js gebruiken

Gebruik de functie `adobe.target.triggerView` . Deze functie kan worden aangeroepen wanneer een nieuwe pagina wordt geladen of wanneer een component op een pagina opnieuw wordt weergegeven. De functie `adobe.target.triggerView()` moet worden geïmplementeerd voor toepassingen van één pagina (SPA&#39;s), zodat [!UICONTROL Visual Experience Composer] (VEC) kan worden gebruikt om [!UICONTROL A/B Test] - en [!UICONTROL Experience Targeting] (XT)-activiteiten te maken. Als `adobe.target.triggerView()` niet op de plaats wordt uitgevoerd, kan VEC niet voor SPAs worden gebruikt.

**Voorbeeld**

```javascript
adobe.target.triggerView("homeView")
```

[Meer informatie](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)

### [!DNL Platform Web SDK] gebruiken

Als u een toepassing op één pagina wilt activeren of signaleren [!UICONTROL View Change] , stelt u de eigenschap `web.webPageDetails.viewName` in onder de optie `xdm` van de opdracht `sendEvent` . De [!DNL Platform Web SDK] controleert de weergavecache als er aanbiedingen zijn voor de `viewName` opgegeven in `sendEvent` , worden deze uitgevoerd en wordt een weergavemeldingsgebeurtenis verzonden.

**Voorbeeld**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  xdm:{
    web:{
      webPageDetails:{
        viewName: "homeView"
      }
    }
  }
});
```

[Meer informatie](/help/dev/implement/client-side/aep-web-sdk/spa-implementation.md)

## Betere benutting [!UICONTROL Response Tokens]

De inhoud van Personalization die van [!DNL Target] is teruggekeerd omvat [ reactietokens ](https://experienceleague.adobe.com/en/docs/target/using/administer/response-tokens). De tekenen van de reactie zijn details over de activiteit, de aanbieding, de ervaring, het gebruikersprofiel, geo informatie, en meer. Deze details kunnen met derdehulpmiddelen worden gedeeld of voor het zuiveren worden gebruikt. De tokens van de reactie kunnen in het [!DNL Target] gebruikersinterface worden gevormd.

### At.js gebruiken

Gebruik aangepaste gebeurtenissen at.js om te luisteren naar de reactie van [!DNL Target] en de reactietokens te lezen.

**Voorbeeld**

```javascript
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(e) { 
  console.log("Request succeeded", e.detail); 
}); 
```

[ Leer meer ](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)

### [!DNL Platform Web SDK] gebruiken

>[!IMPORTANT]
>
>Zorg ervoor dat u [!DNL Experience Platform Web SDK] versie 2.6.0 of hoger gebruikt.

De reactietokens worden geretourneerd als onderdeel van de `propositions` die worden weergegeven in het resultaat van de opdracht `sendEvent` . Elke propositie bevat een array van `items,` en elk item heeft een `meta` -object dat is gevuld met responstokens als deze zijn ingeschakeld in de [!DNL Target] -beheerinterface. [ Leer meer ](https://experienceleague.adobe.com/en/docs/target/using/administer/response-tokens)

**Voorbeeld**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Format of result.propositions:
      /*
        [
            {
                "id": "",
                "scope": "",
                "items": [
                    {
                        "id": "",
                        "schema": "",
                        "data": {},
                        "meta": { // RESPONSE TOKENS
                            "activity.name": ...,
                            "offer.id": ...,
                            "profile.activeActivities": ...
                        }
                    }
                ],
                "scopeDetails": {}
                "renderAttempted": false
            }
        ]
      */
    }
  });
```

[Meer informatie](/help/dev/implement/client-side/aep-web-sdk/accessing-response-tokens.md)

## Flikkering beheren

### At.js gebruiken

Als u at.js gebruikt, kunt u flikkering beheren door `bodyHidingEnabled: true` zo in te stellen dat at.js het bestand is dat zorgt voor
de gepersonaliseerde containers voorverbergen voordat deze de DOM-wijzigingen ophalen en toepassen.

De paginagedeelten die gepersonaliseerde inhoud bevatten, kunnen vooraf worden verborgen door het bestand at.js te overschrijven `bodyHiddenStyle.`

Standaard verbergt `bodyHiddenStyle` de hele HTML `body.`

U kunt beide instellingen overschrijven door `window.targetGlobalSettings.` `window.targetGlobalSettings` te gebruiken voordat u het bestand at.js laadt.

### [!DNL Platform Web SDK] gebruiken

Gebruikend [!DNL Platform Web SDK] kan de klant opstelling hun pre-verbergende stijl in vormen bevel, zoals in het volgende voorbeeld:

```javascript
alloy("configure", {
  datastreamId: "configurationId",
  orgId: "orgId@AdobeOrg",
  debugEnabled: true,
  prehidingStyle: "body { opacity: 0 !important }"
});
```

Wanneer u [!DNL Platform Web SDK] async laadt, raadt [!DNL Adobe] aan het volgende fragment op de pagina in te spuiten voordat [!DNL Platform Web SDK] wordt geïnjecteerd:

```html
<script>
  !function(e,a,n,t){
  if (a) return;
  var i=e.head;if(i){
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
  setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

## Hoe wordt A4T verwerkt?

### At.js gebruiken

Er zijn twee types van registreren A4T die het gebruiken at.js worden gesteund:

* Logboekregistratie aan clientzijde
* Logboekregistratie op de server voor Analytics

#### Logboekregistratie aan clientzijde

**Voorbeeld 1: Het gebruiken van [!DNL Target] Globale Plaatsing**

Logboekregistratie aan de clientzijde van Analytics kan worden ingeschakeld door `analyticsLogging: client_side` in te stellen bij de instellingen at.js of door het `window.targetglobalSettings` -object te overschrijven.

Als deze optie is ingesteld, ziet de indeling van de geretourneerde lading er als volgt uit:

```json
{
  "analytics": {
    "payload": {
      "pe": "tnt",
      "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
    }
  }
}
```

De lading kan dan aan [!DNL Analytics] via [!DNL  Data Insertion API] door:sturen.

Voorbeeld 2: Het vormen het in elke `getOffers` functie:

```javascript
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

Dit codefragment is hoe de antwoordlading eruit ziet:

```json
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

De [!DNL Analytics] nuttige lading (`tnta` teken) zou in de [!DNL Analytics] klap moeten worden omvat gebruikend [ Invoeging API van Gegevens ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md).

#### [!DNL Analytics] Logboekregistratie op de server

[!DNL Analytics] Logboekregistratie aan de serverzijde kan worden ingeschakeld door `analyticsLogging: server_side` in te stellen bij de instellingen at.js of door het `window.targetglobalSettings` -object te overschrijven.

Vervolgens worden de gegevens als volgt gestroomd:

![ Diagram die het Zijhet Registreren werkschema van de Server van de Analyse tonen ](/help/dev/implement/client-side/aep-web-sdk/assets/a4t-server-side-atjs.png)

[ leer meer ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html)

### [!DNL Platform Web SDK] gebruiken

Het web-SDK biedt ook ondersteuning voor:

* Logboekregistratie aan clientzijde
* Logboekregistratie aan de zijde van Analytics Server

#### [!DNL Analytics] Logboekregistratie aan clientzijde

[!DNL Analytics] Logboekregistratie aan de clientzijde wordt ingeschakeld wanneer [!DNL Adobe Analytics] is uitgeschakeld voor die DataStream-configuratie.

![ Diagram die het Analytics Kant Logging werkschema van de Cliënt tonen ](/help/dev/implement/client-side/aep-web-sdk/assets/analytics-disabled-datastream-config.png)

De klant heeft toegang tot het [!DNL Analytics] teken (`tnta`) dat met [!DNL Analytics] moet worden gedeeld gebruikend [ de Invoeging API van Gegevens ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) door het `sendEvent` bevel in een keten te brengen en door de resulterende voorstellingenserie te herhalen.

**Voorbeeld**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  for (var i = 0; i < results.propositions.length; i++) {
    var proposition = results.propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getAnalyticsPayload(proposition);
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // send the page view Analytics hit with collected Analytics payload using Data Insertion API
});
```

Hier volgt een diagram waarin wordt aangegeven hoe gegevens stromen wanneer [!DNL Analytics] Client Side is ingeschakeld:

![ de stroomdiagram van Gegevens in het Zijkbestand van de Cliënt van Analytics ](/help/dev/implement/client-side/aep-web-sdk/assets/analytics-client-side-logging.png)

#### [!DNL Analytics] Logboekregistratie op de server

[!DNL Analytics] Logboekregistratie aan de serverzijde wordt ingeschakeld wanneer [!DNL Analytics] is ingeschakeld voor die DataStream-configuratie.

![ Datastreams UI die de montages van Analytics toont.](/help/dev/implement/client-side/aep-web-sdk/assets/analytics-enabled-datastream-config.png)

Wanneer Logboekregistratie aan serverzijde [!DNL Analytics] is ingeschakeld, wordt de A4T-lading die met [!DNL Analytics] moet worden gedeeld, zodat in de [!DNL Analytics] -rapportage correcte indrukkingen en conversies worden weergegeven, op Edge Network-niveau gedeeld, zodat de klant geen verdere verwerking hoeft te uitvoeren.

Hier is hoe de gegevens in de systemen stromen wanneer de Logging van de Analyse van de Zijde van de Server wordt toegelaten:

![ Diagram die de gegevensstroom in het Loggen van de Analyse van de Server Zijde tonen ](/help/dev/implement/client-side/aep-web-sdk/assets/analytics-server-side-logging.png)

## Globale instellingen instellen [!DNL Target]

### At.js gebruiken

U kunt instellingen in de bibliotheek at.js overschrijven met `window.targetGlobalSettings,` in plaats van de instellingen in de gebruikersinterface van [!DNL Target] te configureren of met REST API&#39;s.

De overschrijving moet worden gedefinieerd voordat om.js wordt geladen of in Beheer > Implementatie > Bewerken op.js-instellingen > Codeinstellingen > Bibliotheekheader.

Voorbeeld:

```javascript
window.targetGlobalSettings = {  
   timeout: 200, // using custom timeout  
   visitorApiTimeout: 500, // using custom API timeout  
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com  
};
```

[ Leer meer ](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html)

### [!DNL Platform Web SDK] gebruiken

Deze functie wordt niet ondersteund in de Web SDK.

## [!DNL Target] Profielkenmerken bijwerken

### At.js gebruiken

**Voorbeeld 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "profile.name": "test",
     "profile.gender": "female"
   },
   success: console.log,
   error: console.error
});
```

**Voorbeeld 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          profileParameters: {
            name: "test",
            gender: "female"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

### [!DNL Platform Web SDK] gebruiken

Als u een [!DNL Target] -profiel wilt bijwerken, gebruikt u de opdracht `sendEvent` en stelt u de eigenschap `data.__adobe.target` in, waarbij de namen van toetsen vooraf worden ingesteld met `profile.`

**Voorbeeld**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Hoe gebruik ik [!DNL Target Recommendations]

### At.js gebruiken

**Voorbeeld 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "entity.name": "T-shirt",
     "entity.id": "1234"
   },
   success: console.log,
   error: console.error
});
```

**Voorbeeld 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          parameters: {
            "entity.name": "T-shirt",
            "entity.id": "1234"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

[ Leer meer ](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-getoffers-atjs-2.html)

### [!DNL Platform Web SDK] gebruiken

Als u [!DNL Recommendations] -gegevens wilt verzenden, gebruikt u de opdracht `sendEvent` en stelt u de eigenschap `data.__adobe.target` in, waarbij de sleutelnamen vooraf worden ingesteld met `entity.`

**Voorbeeld**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.name": "T-shirt",
        "entity.id": "1234"
      }
    }
  }
});
```

## Hoe gebruik ik id&#39;s van derden

### At.js gebruiken

Wanneer u at.js gebruikt, zijn er meerdere manieren om `mbox3rdPartyId` te verzenden met `getOffer,` of `getOffers` :

**Voorbeeld 1**

```javascript
adobe.target.getOffer({
  mbox:"test",
  params:{
    "mbox3rdPartyId": "1234"
  },
  success: console.log,
  error: console.error
});
```

**Voorbeeld 2**

```javascript
adobe.target.getOffers({
    request: {
      id:{
        thirdPartyId: "1234"
      },
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

U kunt de `mbox3rdPartyId` ook instellen in `targetPageParams` of `targetPageParamsAll.`

Bij het instellen van `targetPageParams` worden de aanvragen voor `target-global-mbox` ook wel `pag-lLoad` genoemd.

De aanbeveling moet worden ingesteld met `targetPageParamsAll` zoals deze in elk [!DNL Target] -verzoek wordt verzonden. Het voordeel van `targetPageParamsAll` is dat u de `mbox3rdPartyId` op de pagina één keer kunt definiëren om ervoor te zorgen dat alle [!DNL Target] -aanvragen het juiste resultaat hebben `mbox3rdPartyId.`

```javascript
window.targetPageParamsAll = function() {
      return {
        "mbox3rdPartyId": "1234"
      };
    };
```

```javascript
window.targetPageParams = function() {
  return {
    "mbox3rdPartyId": "1234"
  };
};
```

[ Leer meer ](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetpageparams.html)

### [!DNL Platform Web SDK] gebruiken

[!DNL Platform Web SDK] biedt ondersteuning voor [!DNL Target] id van derden. Er zijn echter nog een paar stappen voor nodig.

Met Identiteitskaart kunnen klanten meerdere identiteiten verzenden. Alle identiteiten worden naamruimte gegeven. Elke naamruimte kan een of meer identiteiten hebben. Een bepaalde identiteit kan als primair worden gemarkeerd. Met deze kennis in mening kunt u zien wat de noodzakelijke stappen aan opstelling voor [!DNL Platform Web SDK] zijn om [!DNL Target] identiteitskaart van de Derde te gebruiken.

1. Stel de naamruimte in die de [!DNL Target] id van derden bevat in de configuratiepagina van de gegevensstroom:

![ Datastreams UI die het gebied van de derde van het Doel tonen namespace ](/help/dev/implement/client-side/aep-web-sdk/assets/mbox3rdpartyid.png)

1. Verzend die naamruimte in elke opdracht `sendEvent` als volgt:

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "identityMap": {
      "TGT3PID": [
        {
          "id": "1234",
          "primary": true
        }
      ]
    }
  }
});
```

## Hoe kan ik eigenschapstokens instellen?

### At.js gebruiken

Wanneer u at.js gebruikt, zijn er twee manieren om de eigenschapstokens in te stellen: met `targetPageParams` of `targetPageParamsAll.` Using `targetPageParams` wordt de eigenschapstoken aan de `target-global-mbox` -aanroep toegevoegd, maar met `targetPageParamsAll` wordt het token aan alle [!DNL Target] -aanroepen toegevoegd:

**Voorbeeld 1**

```javascript
   window.targetPageParamsAll = function() {
      return {
        "at_property": "1234"
      };
    };
```

**Voorbeeld 2**

```javascript
window.targetPageParams = function() {
      return {
        "at_property": "1234"
      };
    };
```

### [!DNL Platform Web SDK] gebruiken

Met [!DNL Platform Web SDK] kunnen klanten de eigenschap op een hoger niveau instellen wanneer ze de configuratie van de gegevensstroom instellen onder de naamruimte [!DNL Adobe Target] :

![ Datastreams UI die de montages van Adobe Target toont.](/help/dev/implement/client-side/aep-web-sdk/assets/at-property-setup.png)

Dit betekent dat elke [!DNL Target] oproep voor die specifieke configuratie van de Stream van Gegevens die bezitstoken bevat.

## Hoe kan ik een voorvoegsel toevoegen aan een box

### At.js gebruiken

Deze functionaliteit is alleen beschikbaar in at.js 2.x. at.js 2.x heeft een nieuwe functie met de naam `getOffers` . Met de functie `getOffers` kunnen klanten inhoud vooraf instellen voor een of meer vakken. Hier volgt een voorbeeld:

```javascript
adobe.target.getOffers({
    request: {
      prefetch: {
        mboxes: [{
          index: 0,
          name: "test-mbox",
          parameters: {
            ...
          },
          profileParameters: {
            ...
          }
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

>[!NOTE]
>
>Adobe raadt aan ervoor te zorgen dat elke `mbox` in de `mboxes` -array een eigen index heeft. Meestal heeft de eerste mbox `index=0` de volgende `index=1,` enzovoort.

### [!DNL Platform Web SDK] gebruiken

Deze functionaliteit wordt momenteel niet ondersteund in [!DNL Platform Web SDK] .

## Hoe kan ik fouten opsporen in mijn [!DNL Target] -implementatie

### At.js gebruiken

De bibliotheek at.js stelt deze het zuiveren eigenschappen bloot:

* Mbox Disable - schakelt [!DNL Target] uit van ophalen en renderen om te controleren of de pagina wordt onderbroken zonder [!DNL Target] interacties
* Mbox Debug - at.js registreert elke actie
* Doelovertrek - met een mbox trace-token gegenereerd in een trace-object met details die aan het beslissingsproces hebben deelgenomen, is beschikbaar onder `window.___target_trace` -object.

>[!NOTE]
>
>Al deze het zuiveren eigenschappen zijn beschikbaar met verbeterde mogelijkheden in [ Adobe Experience Platform Debugger ](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob).

### [!DNL Platform Web SDK] gebruiken

U hebt meerdere mogelijkheden voor foutopsporing wanneer u [!DNL Platform Web SDK] gebruikt:

* Gebruikend [ Assurance ](https://experienceleague.adobe.com/en/docs/experience-platform/assurance/home)
* [ Web SDK toegelaten zuivert ](https://experienceleague.adobe.com/en/docs/experience-platform/assurance/home)
* Het gebruik van [ SDK controlemaakjes van het Web ](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* Gebruik [ Adobe Experience Platform Debugger ](https://experienceleague.adobe.com/en/docs/experience-platform/debugger/home)
* Doelovertrek