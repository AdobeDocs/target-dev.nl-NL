---
keywords: implementatie, javascript-bibliotheek, js, atjs, apparaatbeslissingen, apparaatbeslissingen, ondersteunde functies, $8
description: Meer weten over welke functies worden ondersteund voor [!UICONTROL on-device decisioning].
title: Welke functies worden ondersteund in een beslissing op het apparaat
feature: at.js
exl-id: bdd65658-6c4a-41ae-a222-59c00a11bdac
source-git-commit: 79ffa3f58d780f587fe1202b82d3860395504dfe
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%

---

# Ondersteunde functies voor [!UICONTROL on-device decisioning]

De [!DNL Adobe Target] JS SDK biedt klanten de flexibiliteit om te kiezen tussen prestaties en versheid van gegevens voor beslissingen. Met andere woorden, als het voor u van het grootste belang is om de meest relevante en engaging van gepersonaliseerde inhoud via computerleren te leveren, moet er een live serveroproep worden gedaan. Maar als de prestaties kritischer zijn, moet een on-device en in-memory beslissing worden genomen. Voor [!UICONTROL on-device decisioning] Raadpleeg de volgende secties waarin de functies worden weergegeven die worden ondersteund.

## Ondersteunde activiteitstypen

De volgende tabel geeft aan welke [activiteitstypen](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) door de [Form-based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) of [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) worden ondersteund of niet ondersteund voor [!UICONTROL on-device decisioning].

| Type activiteit | Ondersteund? |
| --- | --- |
| [A/B-test](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | Ja |
| [Automatisch toewijzen](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Nee |
| [Automatisch doel](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) ![Premium](../../../assets/premium.png) | Nee |
| [Multivariatietest](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | Nee |
| [Gericht op ervaring](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | Ja |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) ![Premium](../../../assets/premium.png) | Nee |
| [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) ![Premium](../../../assets/premium.png) | Nee |
| [Activiteiten die gebruikmaken van Analyses voor Doel](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?) (A4T) | Ja |

## Doelgerichtheid publiek

In de volgende tabel wordt aangegeven voor welke publieksregels deze worden ondersteund [!UICONTROL on-device decisioning].

| Auditieregel | Ondersteund? |
| --- | --- |
| [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Ja<P>Bij gebruik van apparaatbeslissingen worden de volgende geografische kenmerken ondersteund:<ul><li>Land/regio</li><li>Plaats</li><li>Breedte</li><li>Lengtegraad</li></ul> |
| [Netwerk](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | Nee |
| [Mobiel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | Nee |
| [Aangepaste parameters](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Ja |
| [Besturingssysteem](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Ja |
| [Sitepagina&#39;s](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Ja |
| [Browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Ja |
| [Bezoekerprofiel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | Nee |
| [verkeersbronnen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | Nee |
| [Tijdschema](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Ja |
| Adobe Experience Cloud-publiek<P>([!DNL Audiences from Adobe Analytics], [!DNL Adobe Audience Manager], en [!DNL Adobe Experience Manager]) | Nee |

### Geo targeting voor [!UICONTROL on-device decisioning]

Minimale vertraging behouden voor [!UICONTROL on-device decisioning] De activiteiten met geo-based publiek, Adobe adviseert u de geo waarden zelf in de vraag te verstrekken aan [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md). Stel het Geo-object in in de context van de aanvraag. Dit betekent vanuit de browser een manier om de locatie van elke bezoeker te bepalen. Bijvoorbeeld, kunt u een IP-aan-Geo raadpleging uitvoeren, gebruikend de dienst u vormt. Sommige hostingproviders, zoals Google Cloud, bieden deze functionaliteit via aangepaste headers in elk `HttpServletRequest`.

```javascript {line-numbers="true"}
window.adobe.target.getOffers({ 
    decisioningMethod: "on-device", 
    request: { 
        context: { 
            geo: { 
                city: "SAN FRANCISCO", 
                countryCode: "US", 
                stateCode: "CA", 
                latitude: 37.75, 
                longitude: -122.4 
            } 
        }, 
        execute: { 
            pageLoad: {} 
        } 
    } 
})
```

Nochtans, als u geen IP-aan-Geo raadplegingen op uw server kunt uitvoeren, maar u wilt nog uitvoeren [!UICONTROL on-device decisioning] for [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) aanvragen die op geo gebaseerde doelgroepen bevatten, wordt dit ook ondersteund. Het nadeel van deze benadering is dat het een verre IP-aan-Geo raadpleging gebruikt, die latentie aan elk toevoegt `getOffers` vraag. Deze latentie moet lager zijn dan een `getOffers` vraag met server-zijbesluit, omdat het een CDN raakt die dicht bij uw server wordt gevestigd. Geef alleen het veld &quot;ipAddress&quot; in het Geo-object op in de context van uw verzoek aan de SDK om de geolocatie van het IP-adres van uw bezoeker op te halen. Als een ander gebied naast &quot;ipAddress&quot;wordt verstrekt, [!DNL Target] SDK haalt de metagegevens voor de geolocatie niet op voor oplossing.

```javascript {line-numbers="true"}
window.adobe.target.getOffers({ 
    decisioningMethod: "on-device", 
    request: { 
        context: { 
            geo: { 
                ipAddress: "127.0.0.1" 
            } 
        }, 
        execute: { 
            pageLoad: {} 
        } 
    } 
})
```

### Toewijzingsmethode

In de volgende tabel wordt aangegeven voor welke toewijzingsmethoden wel of niet steun wordt verleend [!UICONTROL on-device decisioning].

| Toewijzingsmethode | Ondersteund? |
| --- | --- |
| Handmatig | Ja |
| [Automatisch toewijzen aan de beste ervaring](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Nee |
| [Automatisch richten voor persoonlijke ervaringen](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) | Nee |
