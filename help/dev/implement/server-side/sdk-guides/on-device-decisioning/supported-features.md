---
title: Welke functies worden ondersteund in apparaatbeslissingen?
description: Leer hoe u de meest relevante en boeiende persoonlijke inhoud kunt leveren via computerleren via een live servergesprek.
feature: APIs/SDKs
exl-id: 15d9870f-6c58-4da0-bfe5-ef23daf7d273
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 0%

---

# Overzicht van ondersteunde functies

[!DNL Adobe Target]De server-kant SDKs van ontwikkelaars geeft ontwikkelaars de flexibiliteit om tussen prestaties en versheid van gegevens voor besluiten te kiezen. Met andere woorden, als het voor u van het grootste belang is om de meest relevante en engaging van gepersonaliseerde inhoud via computerleren te leveren, moet er een live serveroproep worden gedaan. Maar als de prestaties kritischer zijn, zou een op-apparatenbesluit moeten worden genomen. Voor [!UICONTROL on-device decisioning] voor uw werk kunt u terecht op de volgende lijst met ondersteunde functies :

* Activiteitstypen
* Doelgerichtheid publiek
* Toewijzingsmethode

## Typen activiteiten

De volgende tabel geeft aan welke [activiteitstypen](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=nl-NL) gemaakt met de [Form-based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=nl-NL&) worden ondersteund of niet ondersteund voor [!UICONTROL on-device decisioning].

| Type activiteit | Ondersteund |
| --- | --- |
| [A/B-test](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=nl-NL) | Ja |
| [Automatisch toewijzen](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=nl-NL) | Nee |
| [Automatisch doel](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html?lang=nl-NL) | Nee |
| [Analyses voor doel](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=nl-NL) (A4T) | Ja |
| [Multivariatietest](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html?lang=nl-NL) (MVT) | Nee |
| [Gericht op ervaring](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html?lang=nl-NL) (XT) | Ja |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html?lang=nl-NL) (AP) | Nee |
| [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html?lang=nl-NL) | Nee |


## Doelgerichtheid publiek

In de volgende tabel wordt aangegeven voor welke publieksregels deze worden ondersteund [!UICONTROL on-device decisioning].

| Auditieregel | Apparaatbeslissingen |
| --- | --- |
| [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=nl-NL) | Ja |
| [Netwerk](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=nl-NL) | Nee |
| [Mobiel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=nl-NL) | Nee |
| [Aangepaste parameters](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=nl-NL) | Ja |
| [Besturingssysteem](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=nl-NL) | Ja |
| [Sitepagina&#39;s](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=nl-NL) | Ja |
| [Browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=nl-NL) | Ja |
| [Bezoekerprofiel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=nl-NL) | Nee |
| [verkeersbronnen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=nl-NL) | Nee |
| [Tijdschema](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=nl-NL) | Ja |
| [Experience Cloud publiek](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html?lang=nl-NL) (Soorten publiek uit Adobe Audience Manager, Adobe Analytics en Adobe Experience Manager) | Nee |

### Geo targeting voor [!UICONTROL on-device decisioning]

Om een latentie van bijna nul te handhaven voor [!UICONTROL on-device decisioning] Adobe raadt u aan om de geo-waarden zelf op te geven in de oproep aan `getOffers`. Doe dit door de `Geo` object in het `Context` van het verzoek. Dit betekent dat uw server een manier nodig heeft om de locatie van elke eindgebruiker te bepalen. Bijvoorbeeld, kan uw server een IP-aan-Geo raadpleging uitvoeren, gebruikend de dienst u vormt. Sommige hostingproviders, zoals Google Cloud, bieden deze functionaliteit via aangepaste headers in elk `HttpServletRequest`.

>[!BEGINTABS]

>[!TAB Node.js]

```csharp {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
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

>[!TAB Java]

```javascript {line-numbers="true"}
public class TargetRequestUtils {

    public static Context getContext(HttpServletRequest request) {
        Context context = new Context()
            .geo(ipToGeoLookup(request.getRemoteAddr()))
            .channel(ChannelType.WEB)
            .timeOffsetInMinutes(330.0)
            .address(getAddress(request));
        return context;
    }

    public static Geo ipToGeoLookup(String ip) {
        GeoResult geoResult = geoLookupService.lookup(ip);
        return new Geo()
            .city(geoResult.getCity())
            .stateCode(geoResult.getStateCode())
            .countryCode(geoResult.getCountryCode());
    }

}
```

>[!ENDTABS]

Nochtans, als u niet de capaciteit hebt om IP-aan-Geo raadplegingen op uw server uit te voeren, maar u wilt nog uitvoeren [!UICONTROL on-device decisioning] for `getOffers` aanvragen die op geo gebaseerde doelgroepen bevatten, wordt dit ook ondersteund. Het nadeel van deze benadering is dat het een verre IP-aan-Geo raadpleging zal gebruiken, die latentie aan elk zal toevoegen `getOffers` vraag. Deze latentie moet lager zijn dan een externe vertraging `getOffers` aanroep, aangezien deze een CDN raakt die zich dicht bij uw server bevindt. U moet alleen de `ipAddress` in het veld `Geo` object in het `Context` van uw verzoek, zodat de SDK de geolocatie van het IP-adres van uw gebruiker kan ophalen. Indien een ander veld naast de `ipAddress` wordt verstrekt, [!DNL Target] SDK haalt de metagegevens voor de geolocatie niet op voor oplossing.


>[!BEGINTABS]

>[!TAB Node.js]

```csharp {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
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

>[!TAB Java]

```javascript {line-numbers="true"}
public class TargetRequestUtils {

    public static Context getContext(HttpServletRequest request) {
        Context context = new Context()
            .geo(new Geo().ipAddress(request.getRemoteAddr()))
            .channel(ChannelType.WEB)
            .timeOffsetInMinutes(330.0)
            .address(getAddress(request));
        return context;
    }

}
```

>[!ENDTABS]

## Toewijzingsmethode

In de volgende tabel wordt aangegeven voor welke toewijzingsmethoden wel of niet steun wordt verleend [!UICONTROL on-device decisioning].

| Toewijzingsmethode | Ondersteund |
| --- | --- |
| Handmatig | Ja |
| [Automatisch toewijzen aan de beste ervaring](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=nl-NL) | Nee |
| [Automatisch richten voor persoonlijke ervaringen](https://experienceleague.adobe.com/docs/target/using/activities/auto-target-to-optimize.html?lang=nl-NL) | Nee |
