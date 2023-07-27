---
keywords: server, targetGlobalSettings, targetGlobalSettings, globalSettings, globalsettings, global settings, at.js, functions, function, clientCode, clientcode, serverDomain, serverDomain, cookieDomain, serverstate5, serverstate6, serverstate7, serverstate8, serverstate9, targetGlobalSettings0, targetGlobalSettings1, targetGlobalSettings Settings2, targetGlobalSettings3, targetGlobalSettings4, targetGlobalSettings5, domain, crossDomain, crossdomain, timeout, globalMboxAutoCreate, bezoekorApiTimeout, defaultContentHiddenStyle, defaultContentVisibleStyle, bodyHiddenStyle, bodyHidingEnabled, imsOrgId, secureOnly , overrideMboxEdgeServer, overrideMboxEdgeServerTimeout, cache5, conkiedomain6, conkiedomain7, conkiedomain8, conkiedomain9, crossDomain0, crossDomain1, crossDomain2, crossDomain3, crossDomain4, crossDomain5, optoutEnabled, opt out, kiezersPollingTimeout, dataProviders, Hybrid Personalization, deviceIdLifetime
description: Gebruik de [!UICONTROL targetGlobalSettings()] functie voor de [!DNL Adobe Target] at.js JavaScript-bibliotheek om instellingen te overschrijven in plaats van de [!DNL Target] UI- of REST-API's.
title: Hoe gebruik ik de [!UICONTROL targetGlobalSettings()] Functie?
feature: at.js
exl-id: f6218313-6a70-448e-8555-b7b039e64b2c
source-git-commit: d5d25c6a559dafe446d26cca6c03d8e693cbd508
workflow-type: tm+mt
source-wordcount: '2518'
ht-degree: 0%

---

# [!UICONTROL targetGlobalSettings()]

U kunt instellingen in de bibliotheek at.js overschrijven met `[!UICONTROL targetGlobalSettings()]`, in plaats van deze in de [!DNL Target] UI of via REST API&#39;s.

## Instellingen

U kunt de volgende instellingen overschrijven:

### artifactLocation

* **Type**: String
* **Standaardwaarde**: Geen
* **Beschrijving**: Een volledig gekwalificeerde URL naar de [Artefact van regel voor apparaatbeslissingen](../../../server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)

### bodyHiddenStyle

* **Type**: String
* **Standaardwaarde**: body { opacity: 0 }
* **Beschrijving**: Wordt alleen gebruikt wanneer `globalMboxAutocreate === true` om de kans op flikkering te minimaliseren.

  Zie voor meer informatie [Hoe at.js flikkering beheert](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md).

### bodyHidingEnabled

* **Type**: Boolean
* **Standaardwaarde**: true
* **Beschrijving**: Wordt gebruikt om flikkering te besturen wanneer `target-global-mbox` wordt gebruikt om aanbiedingen te leveren die in de Visuele Composer van de Ervaring worden gecreeerd, die ook als visuele aanbiedingen wordt bekend.

### clientCode

* **Type**: String
* **Standaardwaarde**: Waarde ingesteld via UI.
* **Beschrijving**: Vertegenwoordigt de clientcode.

### cookieDomain

* **Type**: String
* **Standaardwaarde**: Indien mogelijk ingesteld op het bovenste domein.
* **Beschrijving**: Geeft het domein aan dat wordt gebruikt bij het opslaan van cookies.

### crossDomain

* **Type**: String
* **Standaardwaarde**: Waarde ingesteld via UI.
* **Beschrijving**: Geeft aan of interdomeinspatiëring is ingeschakeld. De toegestane waarden zijn afhankelijk van uw versie at.js. Voor at.js v1.*x*, specificeer of de dwars-domeinmogelijkheden zijn `disabled` (browsers stellen alleen cookies in uw domein in (cookies van de eerste partij), `x only` (browsers stellen cookies in [!DNL Target](alleen domein van het domein) of beide door `enabled` (browsers stellen cookies van zowel de eerste als de derde partij in). Geef voor at.js v2.10 en hoger op of de mogelijkheden voor verschillende domeinen `enabled` (browsers stellen cookies van zowel de 1e als de 3de partij in) of `disabled` (browsers kunnen cookies van derden niet instellen).

### cspScriptNonce

* **Type**: Zie [Beveiligingsbeleid voor inhoud](#content-security-policy) hieronder.
* **Standaardwaarde**: Zie [Beveiligingsbeleid voor inhoud](#content-security-policy) hieronder.
* **Beschrijving**: Zie [Beveiligingsbeleid voor inhoud](#content-security-policy) hieronder.

### cspStyleNonce

* **Type**: Zie [Beveiligingsbeleid voor inhoud](#content-security-policy) hieronder.
* **Standaardwaarde**: Zie [Beveiligingsbeleid voor inhoud](#content-security-policy) hieronder.
* **Beschrijving**: Zie [Beveiligingsbeleid voor inhoud](#content-security-policy) hieronder.

### dataProviders

* **Type**: Zie [Gegevensleveranciers](#data-providers) hieronder.
* **Standaardwaarde**: Zie [Gegevensleveranciers](#data-providers) hieronder.
* **Beschrijving**: Zie [Gegevensleveranciers](#data-providers) hieronder.

### determinoningMethod

* **Type**: String
* **Standaardwaarde**: serverzijde
* **Overige waarden**: op apparaat, hybride
* **Beschrijving**: Zie de onderstaande beslissingsmethoden.

  **Beslissingsmethoden**

  met apparaatbesturing, [!DNL Target] introduceert een nieuwe instelling met de naam Decisioning Method, die bepaalt hoe at.js uw ervaringen biedt. De `decisioningMethod` heeft drie waarden: alleen aan serverzijde, alleen op apparaat en hybride. Wanneer `decisioningMethod` is ingesteld in `targetGlobalSettings()`, fungeert het als standaardbeslissingsmethode voor iedereen [!DNL Target] besluiten.

  **Alleen server**:

  Server-kant slechts is de standaardbeslissingsmethode die uit de doos wordt geplaatst wanneer at.js 2.5+ wordt uitgevoerd en op uw Webeigenschappen opgesteld.

  Het gebruiken van server-kant slechts als standaardconfiguratie betekent dat alle besluiten op [!DNL Target] edge network, wat een blokkerende servervraag impliceert. Deze aanpak kan incrementele vertraging introduceren, maar biedt ook aanzienlijke voordelen, zoals de mogelijkheid om deze toe te passen [!DNL Target]&#39;s machine-learningmogelijkheden die onder andere [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html), [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) (AP), en [Automatisch doel](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) activiteiten.

  Bovendien kunt u uw persoonlijke ervaringen verbeteren door [!DNL Target]Het gebruikersprofiel van uw gebruiker, dat door zittingen en kanalen wordt voortgeduurd, kan krachtige resultaten voor uw zaken verstrekken.

  Tot slot laat server-kant slechts u de Adobe Experience Cloud gebruiken en verfijnen publiek dat tegen door Audience Manager en de segmenten van Adobe Analytics kan worden gericht.

  **Alleen op apparaat**:

  Alleen op het apparaat is de beslissingsmethode die moet worden ingesteld in at.js 2.5+ wanneer de beslissing op het apparaat alleen moet worden gebruikt op alle webpagina&#39;s.

  De besluitvorming op het apparaat kan uw ervaringen en verpersoonlijkingsactiviteiten bij het opblazen van snelle snelheid leveren omdat de besluiten van een caching regelartefact worden gemaakt dat al uw activiteiten bevat die voor op-apparaat besluitvorming kwalificeren.

  Zie de sectie met ondersteunde functies voor meer informatie over welke activiteiten in aanmerking komen voor beslissingen op het apparaat.

  Deze beslissingsmethode moet alleen worden gebruikt als de prestaties van essentieel belang zijn voor alle pagina&#39;s waarvoor beslissingen nodig zijn [!DNL Target]. Houd er bovendien rekening mee dat wanneer deze beslissingsmethode wordt geselecteerd, uw [!DNL Target] activiteiten die niet in aanmerking komen voor beslissingen op het apparaat worden niet uitgevoerd of uitgevoerd. De bibliotheek at.js 2.5+ wordt gevormd om het caching regelartefact slechts te zoeken om besluiten te nemen.

  **Hybride**:

  Hybrid is de besluitvormingsmethode die in at.js 2.5+ moet worden geplaatst wanneer zowel op apparaat het besluit als de activiteiten die een netwerkvraag aan [!DNL Adobe Target] Edge-netwerk moet worden uitgevoerd.

  Wanneer u zowel op apparaat beslissingsactiviteiten als server-zijactiviteiten beheert, kan het een beetje gecompliceerd en vervelend zijn wanneer het denken over hoe te om en voorziening op te stellen [!DNL Target] op uw pagina&#39;s. met hybride als beslissingsmethode, [!DNL Target] weet wanneer het een servervraag aan moet maken [!DNL Adobe Target] Het netwerk van de rand voor activiteiten die server-zijuitvoering vereisen, en ook wanneer om slechts op-apparatenbesluiten uit te voeren.

  Het Artefact van JSON-regels bevat metagegevens om at.js te informeren of een box een serveractiviteit heeft die wordt uitgevoerd of een beslissingsactiviteit op het apparaat. Deze beslissingsmethode zorgt ervoor dat activiteiten die u snel wilt laten uitvoeren, worden uitgevoerd via apparaatbeslissingen en voor activiteiten die krachtigere ML-gestuurde personalisatie vereisen, worden deze activiteiten uitgevoerd via de [!DNL Adobe Target] Edge-netwerk.

### defaultContentHiddenStyle

* **Type**: String
* **Standaardwaarde**: zichtbaarheid: verborgen
* **Beschrijving**: Wordt alleen gebruikt voor omsluitende kaders die gebruik maken van DIV met klassenaam &quot;mboxDefault&quot; en die worden uitgevoerd via `mboxCreate()`, `mboxUpdate()`, of `mboxDefine()` om standaardinhoud te verbergen.

### defaultContentVisibleStyle

* **Type**: String
* **Standaardwaarde**: zichtbaarheid: zichtbaar
* **Beschrijving**: Wordt alleen gebruikt voor omsluitende kaders die gebruik maken van DIV met klassenaam &quot;mboxDefault&quot; en die worden uitgevoerd via `mboxCreate()`, `mboxUpdate()`, of `mboxDefine()` om het toegepaste voorstel als om het even welke of standaardinhoud te tonen.

### deviceIdLifetime

* **Type**: Number
* **Standaardwaarde**: 63244800000 ms = 2 jaar
* **Beschrijving**: Hoeveelheid tijd `deviceId` blijft in cookies bestaan.

>[!NOTE]
>
>De instelling deviceIdLifetime kan worden overschreven in at.js versie 2.3.1 of hoger.

### enabled

* **Type**: Boolean
* **Standaardwaarde**: true
* **Beschrijving**: Indien ingeschakeld, wordt een [!DNL Target] verzoek om ervaringen op te halen en DOM-manipulatie om de ervaringen te renderen wordt automatisch uitgevoerd. Bovendien [!DNL Target] de vraag kan manueel via worden uitgevoerd `getOffer(s)` / `applyOffer(s)`.

  Indien uitgeschakeld, [!DNL Target] aanvragen worden niet automatisch of handmatig uitgevoerd.

### globalMboxAutoCreate

* **Type**: Number
* **Standaardwaarde**: Waarde ingesteld via UI.
* **Beschrijving**: Geeft aan of het algemene mbox-verzoek moet worden geactiveerd.

### imsOrgId

* **Type**: String
* **Standaardwaarde**: true
* **Beschrijving**: Vertegenwoordigt de IMS ORG-ID.

### optinEnabled

* **Type**: Boolean
* **Standaardwaarde**: false
* **Beschrijving**: [!DNL Target] biedt ondersteuning voor aanmeldingsfuncties via Adobe Experience Platform om uw strategie voor het beheer van uw toestemming te ondersteunen. De opt-in functionaliteit laat klanten controleren hoe en wanneer [!DNL Target] -tag wordt geactiveerd. Via Adobe Experience Platform is er ook een optie om de [!DNL Target] -tag. De mogelijkheid om Opt-In te gebruiken in het dialoogvenster [!DNL Target] at.js-bibliotheek toevoegen `optinEnabled=true` instellen. In Adobe Experience Platform moet u &quot;inschakelen&quot; selecteren in de vervolgkeuzelijst GDPR Opt-In in de installatieweergave van de extensie. Zie de [Adobe Experience Platform-documentatie](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) voor meer informatie . Zie voor meer informatie over deze instelling in verband met privacy- en gegevensbeschermingsvoorschriften, waaronder de algemene gegevensbeschermingsverordening van de Europese Unie (GDPR) en de California Consumer Privacy Act (CCPA) [Regels inzake privacy en gegevensbescherming](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md).

### optoutEnabled

* **Type**: Boolean
* **Standaardwaarde**: false
* **Beschrijving**: Geeft aan of [!DNL Target] De Bezoeker-API moet aanroepen `isOptedOut()` functie. Dit maakt deel uit van de functie voor apparaatgrafiek.

### overrideMboxEdgeServer

* **Type**: Boolean
* **Standaardwaarde**: true (waar, vanaf at.js versie 1.6.2)
* **Beschrijving**: Geeft aan of we moeten gebruiken `<clientCode>.tt.omtrdc.net` domein of `mboxedge<clusterNumber>.tt.omtrdc.net` domein.

  Als deze waarde waar is, `mboxedge<clusterNumber>.tt.omtrdc.net` domein wordt opgeslagen in een cookie. Werken momenteel niet met [CNAME](/help/dev/before-implement/implement-cname-support-in-target.md) bij gebruik van at.js-versies vóór at.js 1.8.2 en at.js 2.3.1. Als dit voor u een probleem is, kunt u [bijwerken om.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md) naar een nieuwere, ondersteunde versie.

### overrideMboxEdgeServerTimeout

* **Type**: Number
* **Standaardwaarde**: 1860000 => 31 minuten
* **Beschrijving**: Geeft de cookielevensduur aan die de `mboxedge<clusterNumber>.tt.omtrdc.net` waarde.

### pageLoadEnabled

* **Type**: Boolean
* **Standaardwaarde**: true
* **Beschrijving**: Als deze optie is ingeschakeld, haalt u automatisch ervaringen op die moeten worden geretourneerd bij het laden van de pagina.

### pollingInterval

* **Type**: Number
* **Standaardwaarde**: 300000 (vijf minuten in milliseconden)
* **Beschrijving**: Interval dat at.js een nieuwe versie van een op-apparaat beslissingsartefact haalt en het geheime voorgeheugen bijwerkt. 300000 is de minimumwaarde die is toegestaan voor `pollingInterval`.

### secureOnly

* **Type**: Boolean
* **Standaardwaarde**: false
* **Beschrijving**: Geeft aan of at.js alleen HTTPS mag gebruiken of mag schakelen tussen HTTP en HTTPS op basis van het paginaprotocol. Wanneer ingesteld op true, stelt secureOnly ook de kenmerken Secure en SameSite in op het cookie van de box.

### selectorsPollingTimeout

* **Type**: Number
* **Standaardwaarde**: 5000 ms = 5 s
* **Beschrijving**: In at.js 0.9.6, [!DNL Target] geïntroduceerd deze nieuwe instelling die via `targetGlobalSettings`.

  De `selectorsPollingTimeout` het plaatsen vertegenwoordigt hoe lang de cliënt bereid is om op alle die elementen te wachten door selecteurs worden geïdentificeerd om op de pagina te verschijnen.

  De activiteiten die via Visual Experience Composer (VEC) worden gecreeerd hebben aanbiedingen die selecteurs bevatten.

### serverDomain

* **Type**: String
* **Standaardwaarde**: Waarde ingesteld via UI.
* **Beschrijving**: Vertegenwoordigt de [!DNL Target] Edge-server.

### serverState

* **Type**: Zie [Hybride personalisatie](#hybrid-personalization) hieronder.
* **Standaardwaarde**: Zie [Hybride personalisatie](#hybrid-personalization) hieronder.
* **Beschrijving**: Zie [Hybride personalisatie](#hybrid-personalization) hieronder.

### telemetryEnabled

* **Type**: Boolean
* **Standaardwaarde**: true
* **Beschrijving**: Wanneer deze optie is ingeschakeld, verzamelt Adobe het gebruik van de SDK-functie en de telemetriegegevens van de prestaties. Persoonlijke gegevens worden niet verzameld.

### timeout

* **Type**: Number
* **Standaardwaarde**: Waarde ingesteld via UI.
* **Beschrijving**: Vertegenwoordigt de [!DNL Target] time-out randverzoek.

### viewsEnabled {#viewsenabled}

* **Type**: Boolean
* **Standaardwaarde**: true
* **Beschrijving**: Als deze optie is ingeschakeld, worden weergaven automatisch opgehaald wanneer de pagina wordt geladen. Wanneer `triggerView` wordt aangeroepen, worden de toepasselijke weergaven weergegeven in de browser. Als deze optie is uitgeschakeld, worden de weergaven niet opgehaald tijdens het laden van de pagina en `triggerView` doet niets. Weergaven worden ondersteund in at.js 2.*x* alleen.

### bezoekerApiTimeout

* **Type**: Number
* **Standaardwaarde**: 2000 ms = 2 s
* **Beschrijving**: Vertegenwoordigt de time-out voor de visitor-API-aanvraag.

## Gebruik

Deze functie kan worden gedefinieerd voordat at.js wordt geladen of in **Administratie** > **Implementatie** > **Instellingen om.js bewerken** > **Codeinstellingen** > **Bibliotheekkoptekst**.

In het veld Bibliotheekkoptekst kunt u JavaScript in vrije vorm invoeren. De aanpassingscode moet er ongeveer als volgt uitzien:

```javascript {line-numbers="true"}
window.targetGlobalSettings = {
   timeout: 200, // using custom timeout
   visitorApiTimeout: 500, // using custom API timeout
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com
};
```

## Gegevensleveranciers {#data-providers}

Met deze instelling kunnen klanten gegevens verzamelen van externe gegevensleveranciers, zoals Demandbase, BlueKai en aangepaste services, en de gegevens doorgeven aan [!DNL Target] als mbox parameters in het globale mbox verzoek. Het steunt de inzameling van gegevens van veelvoudige leveranciers via async en synchronisatieverzoeken. Op deze manier kunt u flikkering van de standaardpagina-inhoud eenvoudig beheren en onafhankelijke time-outs opnemen voor elke provider om de invloed op de paginaprestaties te beperken

>[!NOTE]
>
>Data Providers vereist op .js 1.3 of hoger.

De volgende video&#39;s bevatten meer informatie:

| Video | Beschrijving |
|--- |--- |
| [Gegevensleveranciers gebruiken in Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/use-data-providers-to-integrate-third-party-data.html) | Gegevensleveranciers zijn een mogelijkheid waarmee u gegevens van derden eenvoudig aan Doel kunt doorgeven. Een derde partij zou een weerdienst, een DMP, of zelfs uw eigen Webdienst kunnen zijn. Vervolgens kunt u deze gegevens gebruiken om een publiek te maken, inhoud te benoemen en het profiel van de bezoeker te verrijken. |
| [Gegevensleveranciers implementeren in Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/implement-data-providers-to-integrate-third-party-data.html) | Implementatiedetails en voorbeelden van het gebruik van Adobe [!DNL Target]DataProviders-functie om gegevens van andere gegevensleveranciers op te halen en door te geven in de [!DNL Target] verzoek. |

De `window.targetGlobalSettings.dataProviders` het plaatsen is een serie van gegevensleveranciers.

Elke gegevensaanbieder heeft de volgende structuur:

| Sleutel | Type | Beschrijving |
|--- |--- |--- |
| name | String | Naam van de provider. |
| versie | String | Versie provider. Deze sleutel zal voor leveranciersevolutie worden gebruikt. |
| timeout | Getal | Geeft de time-out van de provider aan als dit een netwerkaanvraag is.  Deze toets is optioneel. |
| provider | -functie | De functie die de logica voor het ophalen van providergegevens bevat.<p>De functie heeft één vereiste parameter: `callback`. De callback-parameter is een functie die alleen moet worden aangeroepen wanneer de gegevens zijn opgehaald of er een fout optreedt.<p>Callback verwacht twee parameters:<ul><li>fout: geeft aan of er een fout is opgetreden. Als alles OK is, moet deze parameter op null worden ingesteld.</li><li>params: een JSON-object dat de parameters vertegenwoordigt die in een [!DNL Target] verzoek.</li></ul> |

In het volgende voorbeeld wordt getoond waar de gegevensaanbieder de synchronisatie uitvoert:

```javascript {line-numbers="true"}
var syncDataProvider = {
  name: "simpleDataProvider",
  version: "1.0.0",
  provider: function(callback) {
    callback(null, {t1: 1});
  }
};

window.targetGlobalSettings = {
  dataProviders: [
    syncDataProvider
  ]
};
```

After at.js-processen `window.targetGlobalSettings.dataProviders`de [!DNL Target] request will contain a new parameter: `t1=1`.

Hieronder ziet u een voorbeeld van de parameters die u wilt toevoegen aan het dialoogvenster [!DNL Target] De aanvraag wordt opgehaald van een service van derden, zoals Bluekai, Demandbase, enzovoort:

```javascript {line-numbers="true"}
var blueKaiDataProvider = {
   name: "blueKai",
   version: "1.0.0",
   provider: function(callback) {
      // simulating network request
     setTimeout(function() {
       callback(null, {t1: 1, t2: 2, t3: 3});
     }, 1000);
   }
}

window.targetGlobalSettings = {
   dataProviders: [
      blueKaiDataProvider
   ]
};
```

After at.js-processen `window.targetGlobalSettings.dataProviders`de [!DNL Target] request will contain additional parameters: `t1=1`, `t2=2` en `t3=3`.

In het volgende voorbeeld worden gegevensleveranciers gebruikt om API-gegevens voor het weer te verzamelen en te verzenden als parameters in een [!DNL Target] verzoek. De [!DNL Target] de aanvraag bevat aanvullende parameters, zoals `country` en `weatherCondition`.

```javascript {line-numbers="true"}
var weatherProvider = {
      name: "weather-api",
      version: "1.0.0",
      timeout: 2000,
      provider: function(callback) {
        var API_KEY = "caa84fc6f5dc77b6372d2570458b8699";
        var lat = 44.426767399999996;
        var lon = 26.1025384;
        var url = "//api.openweathermap.org/data/2.5/weather?";
        var data = {
          lat: lat,
          lon: lon,
          appId: API_KEY
        }

        $.ajax({
          type: "GET",
                url: url,
          dataType: "json",
          data: data,
          success: function(data) {
            console.log("Weather data", data);
            callback(null, {
              country: data.sys.country,
              weatherCondition: data.weather[0].main
            });
          },
          error: function(err) {
            console.log("Error", err);
            callback(err);
          }
        });
      }
    };

    window.targetGlobalSettings = {
      dataProviders: [weatherProvider]
    };
```

Houd rekening met het volgende wanneer u werkt met de `dataProviders` instellen:

* Als de gegevensleveranciers `window.targetGlobalSettings.dataProviders` asynchroon zijn, worden ze parallel uitgevoerd. De visitor-API-aanvraag wordt uitgevoerd parallel met de functies die aan `window.targetGlobalSettings.dataProviders` een minimale wachttijd toestaan.
* at.js zal niet proberen om de gegevens in het voorgeheugen onder te brengen. Als de gegevensleverancier gegevens slechts één keer haalt, zou de gegevensleverancier ervoor moeten zorgen dat de gegevens in het voorgeheugen wordt opgeslagen en, wanneer de leveranciersfunctie wordt aangehaald, de geheim voorgeheugengegevens voor de tweede aanroeping dienen.

## Beveiligingsbeleid voor inhoud

at.js 2.3.0+ ondersteunt het instellen van Content Security Policy-nonces op SCRIPT- en STYLE-tags die aan het pagina-DOM worden toegevoegd bij het toepassen van de geleverde versie [!DNL Target] voorstellen.

De SCRIPT- en STYLE-nonces moeten worden ingesteld in `targetGlobalSettings.cspScriptNonce` en `targetGlobalSettings.cspStyleNonce` voorafgaand aan het laden van 2.3.0+ te.js. Zie een voorbeeld hieronder:

```javascript {line-numbers="true"}
...
<head>
 <script nonce="<script_nonce_value>">
window.targetGlobalSettings = {
  cspScriptNonce: "<csp_script_nonce_value>",
  cspStyleNonce: "<csp_style_nonce_value>"
};
 </script>
 <script nonce="<script_nonce_value>" src="at.js"></script>
...
</head>
...
```

Na `cspScriptNonce` en `cspStyleNonce` instellingen worden opgegeven, stelt at.js 2.3.0+ deze als nonce-kenmerken in op alle SCRIPT- en STYLE-tags die het aan de DOM toevoegt wanneer het toepassen van [!DNL Target] voorstellen.

## Hybride personalisatie

`serverState` is een instelling die beschikbaar is in at.js v2.2+ en die kan worden gebruikt om de paginaprestaties te optimaliseren bij een hybride integratie van [!DNL Target] is geïmplementeerd. Hybride integratie betekent dat u zowel at.js v2.2+ aan de clientzijde als de Delivery-API of een [!DNL Target] SDK aan de serverzijde om ervaringen te bieden. `serverState` geeft at.js v2.2+ de capaciteit om ervaringen direct van inhoud toe te passen die op de server wordt gehaald en aan de cliënt als deel van de pagina teruggegeven wordt.

### Voorwaarden

U moet een hybride integratie hebben van [!DNL Target].

* **Server-kant**: U moet de opdracht [Leverings-API](/help/dev/implement/delivery-api/overview.md) of [Doel-SDK&#39;s](/help/dev/implement/server-side/sdk-guides/getting-started/getting-started.md).
* **Client-kant**: U moet [at.js versie 2.2 of hoger](/help/dev/implement/client-side/atjs/target-atjs-versions.md).

### Codevoorbeelden

Voor een beter begrip van hoe dit werkt, zie hieronder de codevoorbeelden die u op uw server zou hebben. De code gaat ervan uit dat u de [Doel Node.js SDK](https://github.com/adobe/target-nodejs-sdk).

```javascript {line-numbers="true"}
// First, we fetch the offers via Target Node.js SDK API, as usual
const targetResponse = await targetClient.getOffers(options);
// A successfull response will contain Target Delivery API request and response objects, which we need to set as serverState
const serverState = {
  request: targetResponse.request,
  response: targetResponse.response
};
// Finally, we should set window.targetGlobalSettings.serverState in the returned page, by replacing it in a page template, for example
const PAGE_TEMPLATE = `
<!doctype html>
<html>
<head>
  ...
  <script>
    window.targetGlobalSettings = {
      overrideMboxEdgeServer: true,
      serverState: ${JSON.stringify(serverState, null, " ")}
    };
  </script>
  <script src="at.js"></script>
</head>
...
</html>
`;
// Return PAGE_TEMPLATE to the client ...
```

Een monster `serverState` JSON-object voor weergaveprefetch ziet er als volgt uit:

```javascript {line-numbers="true"}
{
 "request": {
  "requestId": "076ace1cd3624048bae1ced1f9e0c536",
  "id": {
   "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "context": {
   "channel": "web",
   "timeOffsetInMinutes": 0
  },
  "experienceCloud": {
   "analytics": {
    "logging": "server_side",
    "supplementalDataId": "7D3AA246CC99FD7F-1B3DD2E75595498E"
   }
  },
  "prefetch": {
   "views": [
    {
     "address": {
      "url": "my.testsite.com/"
     }
    }
   ]
  }
 },
 "response": {
  "status": 200,
  "requestId": "076ace1cd3624048bae1ced1f9e0c536",
  "id": {
   "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "client": "testclient",
  "edgeHost": "mboxedge21.tt.omtrdc.net",
  "prefetch": {
   "views": [
    {
     "name": "home",
     "key": "home",
     "options": [
      {
       "type": "actions",
       "content": [
        {
         "type": "setHtml",
         "selector": "#app > DIV.app-container:eq(0) > DIV.page-container:eq(0) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(1) > DIV.heading:eq(0) > H1.title:eq(0)",
         "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > H1:nth-of-type(1)",
         "content": "<span style=\"color:#FF0000;\">Latest</span> Products for 2020"
        }
       ],
       "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
       "responseTokens": {
        "profile.memberlevel": "0",
        "geo.city": "dublin",
        "activity.id": "302740",
        "experience.name": "Experience B",
        "geo.country": "ireland"
       }
      }
     ],
     "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
    }
   ]
  }
 }
}
```

Nadat de pagina in de browser is geladen, past at.js alle [!DNL Target] voorstellen van `serverState` onmiddellijk, zonder enige netwerkvraag tegen [!DNL Target] rand. Bovendien prehidt at.js alleen de DOM-elementen waarvoor [!DNL Target] aanbiedingen zijn beschikbaar op de server-kant van de inhoud die is opgehaald, en beïnvloeden zo de prestaties bij het laden van pagina&#39;s en de gebruikerservaring positief.

### Belangrijke opmerkingen

Houd rekening met het volgende wanneer u `serverState`:

* Op dit moment biedt at.js v2.2 alleen ondersteuning voor het aanbieden van ervaringen via serverState voor:

   * VEC-gemaakte activiteiten die worden uitgevoerd bij het laden van de pagina.
   * Vooraf opgehaalde weergaven.

     Bij SPA [!DNL Target] Weergaven en `triggerView()` in de API van at.js, in.js v2.2 geheime voorgeheugens de inhoud voor alle meningen die op de server worden vooraf ingesteld en past deze toe zodra elke Mening via wordt teweeggebracht `triggerView()`, opnieuw zonder om het even welke extra inhoud-haalt vraag te vuren aan [!DNL Target].

   * **Opmerking**: Op dit moment worden selectievakjes die op de server worden opgehaald, niet ondersteund in `serverState`.

* Bij toepassen `serverState` aanbiedingen, waarbij at.js `pageLoadEnabled` en `viewsEnabled` instellingen, zoals aanbiedingen voor het laden van pagina&#39;s, worden niet toegepast als de `pageLoadEnabled` instellen is false.

  Schakel de schakeloptie in als u deze instellingen wilt inschakelen **Beheer > Implementatie > Bewerken > Pagina laden ingeschakeld**.

  ![Instellingen voor Laden van pagina](../../assets/page-load-enabled-setting.png)

* Als u `serverState` en gebruiken `<script>` -tags in de geretourneerde inhoud, controleer of de HTML-inhoud `<\/script>` in plaats van `</script>`. Als u `</script>`, wordt de browser geïnterpreteerd `</script>` als het einde van een inline SCRIPT en kan de pagina HTML afbreken.

### Aanvullende bronnen

Meer informatie over `serverState` werkt, bekijk de volgende middelen:

* [Voorbeeldcode](https://github.com/Adobe-Marketing-Cloud/target-node-client-samples/tree/master/advanced-atjs-integration-serverstate).
* [Toepassing van één pagina (SPA), voorbeeldtoepassing met `serverState`](https://github.com/Adobe-Marketing-Cloud/target-node-client-samples/tree/master/react-shopping-cart-demo).
