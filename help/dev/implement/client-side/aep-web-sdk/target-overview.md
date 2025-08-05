---
title: Gebruik  [!DNL Adobe Target]  met  [!DNL Web SDK]  voor verpersoonlijking.
description: Leer hoe te om gepersonaliseerde inhoud met  [!DNL Experience Platform Web SDK]  terug te geven gebruikend  [!DNL Adobe Target].
feature: AEP Web SDK
source-git-commit: 1fe6adc25604612ed9fa090f1f68c18b9c0bdf63
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 0%

---

# [!DNL Adobe Target] en [!DNL Web SDK] gebruiken voor personalisatie

[!DNL Adobe Experience Platform] [!DNL Web SDK] kan persoonlijke ervaringen die in [!DNL Adobe Target] worden beheerd, leveren en renderen naar het webkanaal. U kunt een redacteur van WYSIWYG gebruiken, genoemd [ Visuele Composer van de Ervaring ](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC), of een niet-visuele interface, [ op vorm-gebaseerde Composer van de Ervaring ](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), om, uw activiteiten en verpersoonlijkingservaringen tot stand te brengen te activeren en te leveren.

>[!IMPORTANT]
>
>Leer hoe te om uw [!DNL Target] implementatie aan [!DNL Experience Platform Web SDK] met [ te migreren Migrate Doel van at.js 2.x aan Experience Platform Web SDK ](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html) leerprogramma.
>
>Leer hoe te om [!DNL Target] voor het eerst met [ uit te voeren Adobe Experience Cloud met het 2} leerprogramma van SDK van het Web {. ](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html) Voor informatie specifiek voor [!DNL Target], zie de tutorial sectie getiteld [ Vastgestelde Doel van de Opstelling met het Web SDK van Experience Platform ](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).

De volgende functies zijn getest en worden momenteel ondersteund in [!DNL Target] :

* [ Tests A/B ](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [ A4T Indruk en omzetting rapporterend ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [ de activiteiten van Automated Personalization ](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [ Ervaring richtend activiteiten ](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [ Multivariate Tests (MVT) ](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [ de activiteiten van Aanbevelingen ](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [ Inheemse de indruk en omzetting van het Doel rapporterend ](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [ Steun VEC ](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Web SDK] systeemdiagram

In het volgende diagram krijgt u inzicht in de workflow voor het bepalen van randen in [!DNL Target] en [!DNL Web SDK] .

![ Diagram van de randbeslissing van Adobe Target met SDK van het Web van Experience Platform ](/help/dev/implement/client-side/aep-web-sdk/assets/target-platform-web-sdk-new.png)

| Bellen | Details |
| --- | --- |
| 1 | Het apparaat laadt de [!DNL Web SDK] . [!DNL Web SDK] verzendt een aanvraag naar de Edge Network met XDM-gegevens, de DataStreams Environment ID, doorgegeven parameters en de Klant-id (optioneel). De pagina (of containers) is vooraf verborgen. |
| 2 | De Edge Network stuurt het verzoek naar de Edge-services om deze te verrijken met de informatie over de bezoeker-id, toestemming en andere context-informatie voor bezoekers, zoals geolocatie en apparaatvriendelijke namen. |
| 3 | De Edge Network verzendt de verrijkte aanpassingsaanvraag naar de [!DNL Target] edge met de parameters Visitor ID en passed-in. |
| 4 | Profielscripts worden uitgevoerd en vervolgens opgenomen in de profielopslag van [!DNL Target] . De opslag van het profiel haalt segmenten van [!UICONTROL Audience Library] (bijvoorbeeld, segmenten die van [!DNL Adobe Analytics] worden gedeeld, [!DNL Adobe Audience Manager], [!DNL Adobe Experience Platform]). |
| 5 | Op basis van URL-aanvraagparameters en -profielgegevens bepaalt [!DNL Target] welke activiteiten en ervaringen moeten worden weergegeven voor de bezoeker voor de huidige paginaweergave en voor toekomstige vooraf ingestelde weergaven. [!DNL Target] stuurt dit vervolgens terug naar de Edge Network. |
| 6 | a. De Edge Network stuurt de personalisatiereactie terug naar de pagina, eventueel met inbegrip van profielwaarden voor extra personalisatie. Gepersonaliseerde inhoud op de huidige pagina wordt zo snel mogelijk weergegeven zonder flikkering van de standaardinhoud.<br> b. De gepersonaliseerde inhoud voor meningen die als resultaat van gebruikersacties in Één enkele Toepassing van de Pagina (SPA) worden getoond wordt in het voorgeheugen ondergebracht zodat kan het onmiddellijk zonder een extra servervraag worden toegepast wanneer de meningen worden teweeggebracht. <br> c. De Edge Network verzendt de bezoeker-id en andere waarden in cookies, zoals toestemming, sessie-id, identiteit, cookie-controle, personalisatie. |
| 7 | De Web SDK stuurt het bericht van het apparaat naar de Edge Network. |
| 8 | De Edge Network stuurt [!UICONTROL Analytics for Target] (A4T) gegevens (metagegevens over activiteit, ervaring en conversie) door naar de [!DNL Analytics] edge. |

## [!DNL Adobe Target] inschakelen

Ga als volgt te werk om [!DNL Target] in te schakelen:

1. Laat [!DNL Target] in uw [ datastream ](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) met de aangewezen cliëntcode toe.
1. Voeg de optie `renderDecisions` toe aan uw gebeurtenissen.

Vervolgens kunt u desgewenst ook de volgende opties toevoegen:

* **`decisionScopes`**: haal specifieke activiteiten op (handig voor activiteiten die zijn gemaakt met de op formulieren gebaseerde composer) door deze optie aan uw gebeurtenissen toe te voegen.
* **[PreHide fragment ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/manage-flicker)**: Verberg slechts bepaalde gedeelten van de pagina.

## De [!UICONTROL Adobe Target] VEC gebruiken

Om VEC met a [!DNL Web SDK] implementatie te gebruiken, installeer en activeer of [ Firefox ](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) of [ de HelperUitbreiding van Chrome ](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension) VEC.

Voor meer informatie, zie [ de helperuitbreiding van de Composer van de Visuele Ervaring ](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) in de *gids van Adobe Target*.

## Aangepaste inhoud renderen

Zie [ teruggevend verpersoonlijkingsinhoud ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content) voor meer informatie.

## Soorten publiek in XDM

Wanneer het bepalen van publiek voor uw [!DNL Target] activiteiten die via [!DNL Web SDK] worden geleverd, [ XDM ](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html) moet worden bepaald en worden gebruikt. Nadat u XDM schema&#39;s, klassen, en de groepen van het schemagebied bepaalt, kunt u een [!DNL Target] publieksregel tot stand brengen die door XDM gegevens voor het richten wordt bepaald. Binnen [!DNL Target] worden XDM-gegevens in de [!UICONTROL Audience Builder] weergegeven als een aangepaste parameter. De XDM wordt geserialiseerd met behulp van puntnotatie (bijvoorbeeld `web.webPageDetails.name` ).

Als u [!DNL Target] -activiteiten hebt met vooraf gedefinieerd publiek dat aangepaste parameters of een gebruikersprofiel gebruikt, worden deze niet correct via de SDK geleverd. In plaats van aangepaste parameters of het gebruikersprofiel te gebruiken, moet u in plaats daarvan XDM gebruiken. Er is echter een out-of-the-box publiek dat zich richt op velden die worden ondersteund via de [!DNL Web SDK] en die geen XDM vereisen. Deze velden zijn beschikbaar in de gebruikersinterface van [!DNL Target] waarvoor geen XDM vereist is:

* Doelbibliotheek
* Geo
* Netwerk
* Besturingssysteem
* Sitepagina&#39;s
* Browser
* verkeersbronnen
* Tijdschema

Voor meer informatie, zie [ Categorieën voor publiek ](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html) in de *gids van Adobe Target*.

### Reactietokens

Reactietokens worden gebruikt om metagegevens naar derden, zoals Google of Facebook, te verzenden. Respontokens worden geretourneerd
in het `meta` -veld in `propositions` > `items` .

Hier volgt een voorbeeld:

```json
{
  "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI2NzM2IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
  "scope": "__view__",
  "scopeDetails": ...,
  "renderAttempted": true,
  "items": [
    {
      "id": "0",
      "schema": "https://ns.adobe.com/personalization/dom-action",
      "meta": {
        "experience.id": "0",
        "activity.id": "126736",
        "offer.name": "Default Content",
        "offer.id": "0"
      }
    }
  ]
}
```

Als u de reactietokens wilt verzamelen, moet u zich abonneren op `alloy.sendEvent` promise, `propositions` doorlopen en de details uit `items` -> `meta` extraheren.

Elke `proposition` heeft een `renderAttempted` booleaans veld dat aangeeft of de `proposition` is gerenderd of niet. Zie het onderstaande voorbeeld:

```js
alloy("sendEvent",
  {
    "renderDecisions": true,
    "decisionScopes": [
      "hero-container"
    ]
  }).then(result => {
    const { propositions } = result;

    // filter rendered propositions
    const renderedPropositions = propositions.filter(proposition => proposition.renderAttempted === true);

    // collect the item metadata that represents the response tokens
    const collectMetaData = (items) => {
      return items.filter(item => item.meta !== undefined).map(item => item.meta);
    }

    const pageLoadResponseTokens = renderedPropositions
      .map(proposition => collectMetaData(proposition.items))
      .filter(e => e.length > 0)
      .flatMap(e => e);
  });
  
```

Wanneer automatische rendering is ingeschakeld, bevat de proposities-array:

#### Bij laden van pagina:

* Op formulier gebaseerde composer `propositions` met `renderAttempted` -markering ingesteld op `false`
* Op Visual Experience Composer gebaseerde voorstellingen waarbij de markering `renderAttempted` is ingesteld op `true`
* Op Visual Experience Composer gebaseerde voorstellingen voor een weergave van één pagina-toepassing waarbij de markering `renderAttempted` is ingesteld op `true`

#### Bij weergave - wijzigen (voor weergaven in cache):

* Op Visual Experience Composer gebaseerde voorstellingen voor een weergave van één pagina-toepassing waarbij de markering `renderAttempted` is ingesteld op `true`

Wanneer automatische rendering is uitgeschakeld, bevat de proposities-array:

#### Bij laden van pagina:

* [!DNL Form-based Composer] -based `propositions` with `renderAttempted` -markering ingesteld op `false`
* [!DNL Visual Experience Composer] -gebaseerde voorstellingen waarvoor de markering `renderAttempted` is ingesteld op `false`
* Op [!DNL Visual Experience Composer] gebaseerde voorstellingen voor een toepassingsweergave van één pagina met de markering `renderAttempted` ingesteld op `false`

#### Bij weergave - wijzigen (voor weergaven in cache):

* Op Visual Experience Composer gebaseerde voorstellingen voor een weergave van één pagina-toepassing waarbij de markering `renderAttempted` is ingesteld op `false`

### Eén profiel bijwerken

Met [!DNL Web SDK] kunt u het profiel als een ervaringsgebeurtenis bijwerken naar het [!DNL Target] -profiel en [!DNL Web SDK] .

Als u een [!DNL Target] -profiel wilt bijwerken, moet u ervoor zorgen dat de profielgegevens worden doorgegeven met het volgende:

* Onder `"data {"`
* Onder `"__adobe.target"`
* Voorvoegsel `"profile."`

| Sleutel | Type | Beschrijving |
| --- | --- | --- |
| `renderDecisions` | Boolean | Instrueert de personaliseringscomponent of het DOM acties zou moeten interpreteren |
| `decisionScopes` | Array `<String>` | Een lijst van werkingsgebied om besluiten voor terug te winnen |
| `xdm` | Object | Gegevens geformatteerd in XDM die in Web SDK als ervaringsgebeurtenis landen |
| `data` | Object | Willekeurige sleutel/waardeparen die naar [!DNL Target] oplossingen onder de doelklasse worden verzonden. |

<!--Typical [!DNL Web SDK] code using this command looks like the following:-->

**de reddingsProfiel van de vertraging of entiteitsparameters tot de inhoud aan het eind - gebruiker** is getoond

Als u opnamekenmerken in het profiel wilt vertragen totdat de inhoud is weergegeven, stelt u `data.adobe.target._save=false` in uw verzoek in.

Uw website bevat bijvoorbeeld drie beslissingsbereiken die overeenkomen met drie categorielink op de website (Men, Vrouwen en Kinderen) en u wilt de categorie bijhouden die de gebruiker uiteindelijk heeft bezocht. Verzend deze aanvragen met de markering `__save` ingesteld op `false` om te voorkomen dat de categorie blijft bestaan op het moment dat de inhoud wordt opgevraagd. Nadat de inhoud is weergegeven, verzendt u de juiste lading (inclusief de `eventToken` en `stateToken` ) voor de overeenkomende kenmerken die moeten worden opgenomen.

In het onderstaande voorbeeld wordt een bericht in de stijl trackEvent verzonden, worden profielscripts uitgevoerd, worden kenmerken opgeslagen en wordt de gebeurtenis direct vastgelegd.

```js
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": { /* Experience Event XDM data */ },
    "data": {
        "__adobe": {
            "target": {
                " __save": true|false,
                //defaults to true if omitted
                "profile.gender": "female",
                "profile.age": 30,
                "entity.name": "T-shirt",
                "entity.id": "1234"
            }
        }
    }
})
```

>[!NOTE]
>
>Als de aanwijzing `__save` wordt weggelaten, gebeurt het opslaan van de profiel- en entiteitskenmerken direct. De instructie `__save` is alleen relevant voor profielkenmerken en entiteitsdetails.

## Aanbevelingen aanvragen

In de volgende tabel worden de [!DNL Recommendations] -kenmerken weergegeven en wordt aangegeven of elk kenmerk wordt ondersteund via [!DNL Web SDK] :

| Categorie | Kenmerk | Ondersteuningsstatus |
| --- | --- | --- |
| Aanbevelingen - Standaardentiteitskenmerken | entity.id | Ondersteund |
|  | entity.name | Ondersteund |
|  | entity.categoryId | Ondersteund |
|  | entity.pageUrl | Ondersteund |
|  | entity.thumbnailUrl | Ondersteund |
|  | entity.message | Ondersteund |
|  | entity.value | Ondersteund |
|  | entity.inventory | Ondersteund |
|  | entity.brand | Ondersteund |
|  | entity.margin | Ondersteund |
|  | entity.event.detailsOnly | Ondersteund |
| Aanbevelingen - Aangepaste entiteitskenmerken | entity.yourCustomAttributeName | Ondersteund |
| Aanbevelingen - Gereserveerde parameters mbox/page | excludeIds | Ondersteund |
|  | cartIds | Ondersteund |
|  | productPurchasedId | Ondersteund |
| Pagina of itemcategorie voor categorie affiniteit | user.categoryId | Ondersteund |

**hoe te om de attributen van Aanbevelingen naar [!DNL Target] te verzenden:**

```js
alloy("sendEvent", {
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## Mbox-omzettingscijfers weergeven {#display-mbox-conversion-metrics}

In het onderstaande voorbeeld ziet u hoe u de conversies van weergavekaders kunt bijhouden en profielparameters kunt verzenden naar [!DNL Target] zonder dat u hiervoor in aanmerking hoeft te komen.

```js
alloy("sendEvent", {
    "xdm": {
        "_experience": {
            "decisioning": {
                "propositions": [{
                    "scope": "conversion-step-1" //example scope name
                }],
                "propositionEventType": {
                    "display": 1
                }
            }
        },
        "eventType": "decisioning.propositionDisplay"
    }
});
```


| Eigenschap | Beschrijving |
|---------|----------|
| `xdm._experience.decisioning.propositions[x].scope` | Het werkingsgebied om succesmetrisch met te associëren (die het aan een specifieke activiteit aan de kant van het Doel zal toeschrijven). |
| `xdm._experience.decisioning.propositions[x].eventType` | Een tekenreeks die het bedoelde gebeurtenistype beschrijft. Stel dit in op `"decisioning.propositionDisplay"` voor dit gebruik. |

## Foutopsporing

mboxTrace en mboxDebug zijn vervangen. Gebruik in plaats hiervan een methode van [ het zuiveren van SDK van het Web ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/use-cases/debugging).

## Terminologie

**Voorstellen**: In [!DNL Target], correleren de voorstellen aan de ervaring die van een activiteit wordt geselecteerd.

**Schema**: Het schema van een besluit is het type van aanbieding in [!DNL Target].

**Reikwijdte**: Het werkingsgebied van het besluit. In [!DNL Target] is het bereik de mbox. Het algemene mbox is het bereik `__view__` .

**XDM**: XDM wordt geserialiseerd in puntaantekening en dan gezet in [!DNL Target] als mbox parameters.
