---
title: Logboekregistratie op de client voor A4T-gegevens in de Experience Platform Web SDK
description: Leer hoe te om cliënt-zijregistreren voor Adobe Analytics voor Doel (A4T) toe te laten gebruikend het Web SDK van Experience Platform.
seo-title: Client-side logging for A4T data in the Experience Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: doel;a4t;registreren;web sdk;ervaring;platform;
feature: Implementation
source-git-commit: 4d4ca7dcffdbaee5770084bd85c3109df0d6a8d4
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---

# Logboekregistratie op de client voor A4T-gegevens in de [!DNL Experience Platform Web SDK]

[!DNL Adobe Experience Platform Web SDK] staat u toe om [ Adobe Analytics voor Doel (A4T) ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) gegevens over de cliëntkant van uw Webtoepassing te verzamelen.

Logboekregistratie aan de clientzijde betekent dat relevante [!DNL Target] gegevens worden geretourneerd aan de clientzijde, zodat u gegevens kunt verzamelen en delen met [!DNL Analytics] . Deze optie zou moeten worden toegelaten als u van plan bent gegevens aan Analytics manueel te verzenden gebruikend de [ Invoeging API van Gegevens ](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html).

>[!NOTE]
>
>Een methode om dit uit te voeren gebruikend [ AppMeasurement.js ](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html) is momenteel in ontwikkeling en zal in de nabije toekomst beschikbaar zijn.

In dit document worden de stappen beschreven voor het instellen van A4T-logboekregistratie op de client voor [!DNL Platform Web SDK] en worden voorbeelden gegeven van implementatie voor veelvoorkomende gebruiksgevallen.

## Vereisten {#prerequisites}

In deze zelfstudie wordt ervan uitgegaan dat u bekend bent met de fundamentele concepten en processen die betrekking hebben op het gebruik van [!DNL Platform Web SDK] voor verpersoonlijkingsdoeleinden. Raadpleeg de volgende documentatie als u een inleiding nodig hebt:

* [ Vormend het Web SDK ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/overview)
* [ Verzendende gebeurtenissen ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/sendevent/overview)
* [ teruggevend verpersoonlijkingsinhoud ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## Logboekregistratie op de client instellen [!DNL Analytics] {#set-up-client-side-logging}

In de volgende subsecties wordt beschreven hoe u [!DNL Analytics] logboekregistratie op de client voor uw [!DNL Platform Web SDK] -implementatie kunt inschakelen.

### Enable [!DNL Analytics] client-side log {#enable-analytics-client-side-logging}

Om [!DNL Analytics] cliënt-zijregistreren te overwegen die voor uw implementatie wordt toegelaten, moet u de [!DNL Adobe Analytics] configuratie in uw [ datastream ](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) onbruikbaar maken.

![ de configuratie van de Analyse gegevensstroom gehandicapte ](/help/dev/implement/a4t/assets/disable-analytics-datastream.png)

### [!DNL A4T] -gegevens ophalen van de SDK en verzenden deze naar [!DNL Analytics] {#a4t-to-analytics}

Deze rapportmethode werkt alleen correct als u de [!DNL A4T] verwante gegevens verzendt die zijn opgehaald uit de opdracht [`sendEvent` ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/sendevent/overview) in de hit [!DNL Analytics] .

Wanneer [!DNL Target] Edge een reactie op een voorstel berekent, wordt gecontroleerd of [!DNL Analytics] logboekregistratie op de client is ingeschakeld (bijvoorbeeld als [!DNL Analytics] is uitgeschakeld in uw gegevensstroom). Als logboekregistratie op de client is ingeschakeld, voegt het systeem een [!DNL Analytics] token toe aan elke propositie in de reactie.

De stroom ziet er ongeveer als volgt uit:

![ cliënt-kant registrerenstroom ](/help/dev/implement/a4t/assets/analytics-client-side-logging.png)

Hieronder ziet u een voorbeeld van een `interact` -reactie als [!DNL Analytics] logboekregistratie op de client is ingeschakeld. Als het voorstel betrekking heeft op een activiteit die [!DNL Analytics] rapporteert, heeft het de eigenschap `scopeDetails.characteristics.analyticsToken` .

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
              "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
              "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "characteristics": {
              "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
              "analyticsToken": "434689:0:0|32767"
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Voorstellen voor [!UICONTROL Form-based Experience Composer] -activiteiten kunnen zowel inhoud bevatten als metrische items onder hetzelfde voorstel klikken. In plaats van één analysetoken voor inhoudsweergave in de eigenschap `scopeDetails.characteristics.analyticsToken` , kunnen er dus zowel een display- als een click-analysetoken worden opgegeven in de eigenschappen `scopeDetails.characteristics.analyticsDisplayToken` en `scopeDetails.characteristics.analyticsClickToken` .

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
               "displayToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
               "clickToken": "E0gb6q1+WyFW3FMbbQJmrg==",
               "analyticsDisplayToken": "434689:0:0|2,434689:0:0|1", 
               "analyticsClickToken": "434689:0:0|32767"
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
            },
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Alle waarden van `scopeDetails.characteristics.analyticsToken`, evenals `scopeDetails.characteristics.analyticsDisplayToken` (voor getoonde inhoud) en `scopeDetails.characteristics.analyticsClickToken` (voor klikmetriek) zijn de nuttige ladingen A4T die moeten worden verzameld en als `tnta` markering in de [ API van de Invoeging van Gegevens ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) vraag worden omvat.

>[!IMPORTANT]
>
>De eigenschappen `analyticsToken`, `analyticsDisplayToken`, `analyticsClickToken` kunnen meerdere tokens bevatten, samengevoegd als één door komma&#39;s gescheiden tekenreeks.
>
>In de implementatievoorbeelden in de volgende sectie worden meerdere [!DNL Analytics] tokens intern verzameld. Als u een array van [!DNL Analytics] tokens wilt aaneenschakelen, gebruikt u een soortgelijke functie:
>
>```javascript
>var concatenateAnalyticsPayloads = function concatenateAnalyticsPayloads(analyticsPayloads) {
>   if (analyticsPayloads.size > 1) {
>       return [].concat(analyticsPayloads).join(',');
>   }
>   return [].concat(analyticsPayloads).join();
>};
>```

## Voorbeelden van implementaties {#implementation-examples}

In de volgende subsecties ziet u hoe u [!DNL Analytics] -logboekregistratie op de client implementeert voor veelvoorkomende gebruiksgevallen.

### [!UICONTROL Form-Based Experience Composer] activiteiten {#form-based-composer}

U kunt [!DNL Platform Web SDK] gebruiken om de uitvoering van voorstellen van [ Adobe Target vorm-Gebaseerde Composer van de Ervaring te controleren ](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) activiteiten.

Wanneer u om voorstellen voor een specifiek besluitwerkingsgebied verzoekt, bevat het teruggekeerde voorstel zijn aangewezen [!DNL Analytics] teken. De beste manier is om de opdracht [!DNL Experience Platform Web SDK] `sendEvent` te koppelen en de geretourneerde voorstellen te doorlopen om deze uit te voeren terwijl de [!DNL Analytics] -tokens tegelijkertijd worden verzameld.

U kunt een opdracht `sendEvent` activeren voor een [!UICONTROL Form-Based Experience Composer] activity scope zoals:

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  for (var i = 0; i < results.propositions.length; i++) {
    //Execute the propositions and collect the Analytics payload
  }
});
```

Vanaf hier moet u code implementeren om de voorstellingen uit te voeren en een lading samen te stellen die uiteindelijk naar [!DNL Analytics] wordt verzonden. Dit is een voorbeeld van wat `results.propositions` kan bevatten:

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
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
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
        "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
        "analyticsToken": "434689:0:0|32767"
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
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434688"
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
          "displayToken": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "clickToken": "Tagb6q1+WyFW3FMbbQJrtg==",
          "analyticsDisplayTokens": "434688:0:0|2,434688:0:0|1",
          "analyticsClickTokens": "434688:0:0|32767"
        }
      }
    },
    "items": [
      {
        "id": "1184845",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434688",
          "experience.id": "0",
          "activity.name": "a4t test form based activity 1",
          "offer.id": "1184845"
        },
        "data": {
          "id": "1184845",
          "format": "text/html",
          "content": "<div> analytics impressions 1</div>"
        }
      },
      {
        "id": "434688",
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

Als u het token [!DNL Analytics] wilt extraheren uit een voorstel met inhoudsitems, kunt u een functie implementeren die lijkt op het volgende:

```javascript
function getDisplayAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsDisplayToken) {
    return characteristics.analyticsDisplayToken;
  }
  return characteristics.analyticsToken;
}
```

Een voorstel kan verschillende soorten punten hebben, zoals die door het `schema` bezit van het punt in kwestie worden vermeld. Er zijn vier schema&#39;s voor propositie-items die worden ondersteund voor [!UICONTROL Form-Based Experience Composer] -activiteiten:

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` en `JSON_SCHEMA` zijn de schema&#39;s die het type van de aanbieding weerspiegelen, terwijl `MEASUREMENT_SCHEMA` de metriek weerspiegelt die aan een DOM element zou moeten worden vastgemaakt.

[!DNL Analytics] nuttige ladingen voor klikmetriek zouden moeten worden verzameld en naar [!DNL Analytics] worden verzonden gescheiden van inhoudspunten, op het ogenblik dat de bezoeker eigenlijk de eerder getoonde inhoud klikt.

De volgende hulpfunctie voor het krijgen van de klik metrische A4T nuttige lasten komt in dit geval in handvat:

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsClickToken) {
    return characteristics.analyticsClickToken;
  }
  return characteristics.analyticsToken;
}
```

#### Overzicht van implementatie {#implementation-summary}

Samenvattend, moeten de volgende stappen worden uitgevoerd wanneer u [!UICONTROL Form-Based Experience Composer] -activiteiten toepast met [!DNL Experience Platform Web SDK] :

1. Verzend een gebeurtenis die [!UICONTROL Form-Based Experience Composer] activity-aanbiedingen ophaalt.
1. Pas de inhoudswijzigingen toe op de pagina;
1. Verzend de `decisioning.propositionDisplay` notification-gebeurtenis;
1. Verzamel de [!DNL Analytics] weergavetokens van de SDK-reactie en construeer een payload voor de [!DNL Analytics] hit.
1. Verzend de nuttige lading naar [!DNL Analytics] gebruikend de [ Invoeging API van Gegevens ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);
1. Als er klikmetriek in geleverde voorstellen zijn, zouden de klikluisteraars opstelling moeten zijn zodat wanneer een klik wordt uitgevoerd, het de `decisioning.propositionInteract` berichtgebeurtenis verzendt. De `onBeforeEventSend` -handler moet zo worden geconfigureerd dat bij het onderscheppen van `decisioning.propositionInteract` -gebeurtenissen de volgende handelingen plaatsvinden:
   1. De kliktokens [!DNL Analytics] van `xdm._experience.decisioning.propositions` verzamelen
   1. Verzenden van de klik [!DNL Analytics] slag met de verzamelde [!DNL Analytics] nuttige lading via [ de Invoeging API van Gegevens ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  var analyticsPayload = new Set();
  results.propositions.forEach(function (proposition) {
    proposition.items.forEach(function (item) {
      if (item.schema === HTML_SCHEMA) {
        // 1. Apply offer
        // 2. Collect executed propositions and send the decisioning.propositionDisplay notification event
        // 3. Collect the display Analytics tokens
      }
      if (item.schema === MEASUREMENT_SCHEMA) {
        // Setup click listener, so that when clicked:
        // 1. Collect clicked propositions and send the decisioning.propositionInteract notification event
        // Note: onBeforeEventSend handler should be configured, so that when intercepting decisioning.propositionInteract events:
        //   1. Collect the click Analytics tokens from xdm._experience.decisioning.propositions
        //   2. Send the click Analytics hit with the collected Analytics payload via Data Insertion API
      }
    });
  });
  // Send the page view Analytics hit with the collected display Analytics payload via Data Insertion API
});
```

### [!UICONTROL Visual Experience Composer] (VEC)-activiteiten {#visual-experience-composer-acitivties}

[!DNL Platform Web SDK] staat u toe om aanbiedingen te behandelen die gebruikend [ Visuele Composer van de Ervaring (VEC) ](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) werden authored.

>[!NOTE]
>
>De stappen voor het uitvoeren van dit gebruiksgeval zijn zeer gelijkaardig aan de stappen voor [ op vorm-Gebaseerde activiteiten van de Composer van de Ervaring ](#form-based-composer). Bekijk de vorige sectie voor meer informatie.

Wanneer automatische rendering is ingeschakeld, kunt u de [!DNL Analytics] tokens verzamelen van de voorstellingen die op de pagina zijn uitgevoerd. De beste manier is om de opdracht [!DNL Experience Platform Web SDK] `sendEvent` te koppelen en de geretourneerde voorstellen te doorlopen om de voorstellen te filteren die de Web SDK heeft gerenderd.

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
  
    var proposition = propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getDisplayAnalyticsPayload(proposition);
      
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // Send the page view Analytics hit with collected Analytics payload via Data Insertion API
});
```

### Werken met `onBeforeEventSend` voor het verwerken van paginageometrische gegevens {#using-onbeforeeventsend}

Met behulp van [!DNL Adobe Target] -activiteiten kunt u verschillende metriek instellen op de pagina, handmatig gekoppeld aan het DOM of automatisch gekoppeld aan het DOM (VEC-authored activiteiten). Beide typen vormen een vertraagde interactie van de eindgebruiker op de webpagina.

Hiervoor kunt u het beste [!DNL Analytics] -ladingen verzamelen met de `onBeforeEventSend` [!DNL Adobe Experience Platform Web SDK] -haak. De `onBeforeEventSend` haak moet worden geconfigureerd met de opdracht `configure` en wordt weerspiegeld in alle gebeurtenissen die door de gegevensstroom worden verzonden.

Hieronder ziet u hoe `onBeforeEventSent` kan worden geconfigureerd om [!DNL Analytics] -hits te activeren:

```javascript
alloy("configure", {
  datastreamId: "datastream configuration ID",
  orgId: "adobe ORG ID",
  onBeforeEventSend: function(options) {
    const xdm = options.xdm;
    const eventType = xdm.eventType;
    if (eventType === "decisioning.propositionInteract") {
      const analyticsPayloads = new Set();
      const propositions = xdm._experience.decisioning.propositions;

      for (var i = 0; i < propositions.length; i++) {
        var proposition = propositions[i];
        analyticsPayloads.add(getClickAnalyticsPayload(proposition));
      }
      // Trigger the Analytics hit
    }
  }
});
```

## Volgende stappen {#next-steps}

Deze handleiding betrof het aanmelden van gegevens op de client voor A4T-gegevens in de [!DNL Platform Web SDK] . Zie de gids op [ server-zijregistreren ](/help/dev/implement/a4t/server-side-a4t.md) voor meer informatie over hoe te om A4T gegevens over Edge Network te behandelen.