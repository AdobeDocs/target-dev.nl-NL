---
title: Doelgerichtheid publiek
description: Het publiek kan worden gebruikt om uw experimenten en verpersoonlijkingsactiviteiten te richten. [!DNL Adobe Target] biedt ondersteuning voor een groot aantal krachtige doelgroepen die hun mogelijkheden uit de box willen halen.
exl-id: df1bd856-e848-452c-90a0-abf29e7a2313
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 0%

---

# Doelgerichtheid publiek

## Overzicht

Het publiek kan worden gebruikt om uw experimenten en verpersoonlijkingsactiviteiten te richten. [!DNL Adobe Target] biedt ondersteuning voor een groot aantal krachtige doelgroepen die hun mogelijkheden uit de box willen halen. De volgende kenmerken zijn beschikbaar voor [doelgerichte doelgroep](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/create-audience.html):

### [!DNL Target] Bibliotheek

Zie voor meer informatie [[!DNL Target] Bibliotheek](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-library.html). &#x200B;
* Verwezen van Bing
* Chrome-browser
* Firefox-browser
* Verwezen vanuit Google
* Internet Explorer
* Linux besturingssysteem
* Mac OS-besturingssysteem
* Nieuwe bezoekers
* Bezoekers terugsturen
* Safari Browser
* Tabletapparaat
* Windows-besturingssysteem
* Verwezen vanuit Yahoo

### Geo

Zie voor meer informatie [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html). &#x200B; &#x200B;
* Land/regio
* Staat
* Plaats
* Postcode
* Breedte
* Lengtegraad
* DMA
* Mobiele vervoerder

### Netwerk

Zie voor meer informatie [Netwerk](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html).

* ISP
* Domeinnaam
* Verbindingssnelheid

### Mobiel

Zie voor meer informatie [Mobiel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html).

* Marketingnaam apparaat
* Apparaatmodel
* Leverancier van apparaat
* Is een mobiel apparaat
* Is mobiele telefoon
* Is tablet
* OS
* Schermhoogte (px)
* Schermbreedte (px)

### Aangepast

Zie voor meer informatie [Aangepaste parameters](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html).

* een sleutel/waardepaar

### Besturingssysteem

Zie voor meer informatie [Besturingssysteem](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html).

* Linux
* Macintosh
* Windows

### Sitepagina&#39;s

Zie voor meer informatie [Sitepagina&#39;s](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html).

* Huidige pagina
* Vorige pagina
* Openingspagina
* HTTP-header

### Browser

Zie voor meer informatie [Browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html).

* Type
* Taal
* Versie

### Bezoekerprofiel

Zie voor meer informatie [Bezoekerprofiel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html).

* om het even welk sleutel/waardepaar, dat wordt voortgeduurd

### verkeersbronnen

Zie voor meer informatie [verkeersbronnen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html).

* Van Baidu
* Vanaf band
* Van Google
* Van Yahoo
* Referentie bestemmingspagina: URL
* Referentie bestemmingspagina: domein
* Verwijzen naar bestemmingspagina: query

### Tijdschema

Zie voor meer informatie [Tijdschema](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html).

* Begindatum / Einddatum

## Clienttips

[!DNL Adobe Target] Vereist de Tips van de Cliënt voor correcte segmentatie van Browser, Werkende Systeem, en Mobiele publieksattributen, evenals bepaalde instanties van de Manuscripten van het Profiel. Zie voor meer achtergrondinformatie [Gebruikersagent en clienttips](../../../client-side/atjs/user-agent-and-client-hints.md).

### Clienttips doorgeven aan [!DNL Adobe Target]

Vanaf Node.js SDK v2.4.0 en Java SDK v2.3.0 kan de Tips van de Cliënt naar worden verzonden [!DNL Target] via `getOffers()` oproepen. De wenken van de cliënt zouden op de `request.context` samen met Gebruikersagent.

>[!BEGINTABS]

>[!TAB Node.js SDK]

```js {line-numbers="true"}
targetClient.getOffers({ 
    request: { 
        context: { 
            channel: "mobile" 
            userAgent: "Mozilla/5.0 (Linux; Android 12; Pixel 4a) AppleWebKit/537.36 (KHTML, like Gecko) Mobile Safari/537.36", 
            clientHints: { 
                mobile: "true", 
                platform: "Linux", 
                platformVersion: "12.1", 
                model: "Pixel 4a", 
                browserUAWithMajorVersion: "\"Not A;Brand\";v=\"98\", \"Chromium\";v=\"98\", \"Google Chrome\";v=\"98\"", 
                browserUAWithFullVersion: "\" Not A;Brand\";v=\"98.0.0.0\", \"Chromium\";v=\"98.0.4844.83\", \"Google Chrome\";v=\"98.0.4758.101\"", 
                bitness: "64", 
                architecture: "x86" 
            } 
        }, 
        execute: { 
            mboxes: [{ 
                name: "home", 
                index: 1 
            }] 
        } 
    } 
});
```

>[!TAB Java SDK]

```javascript {line-numbers="true"}
import com.adobe.target.delivery.v1.model.ClientHints; 
import com.adobe.target.delivery.v1.model.Context; 
import com.adobe.target.delivery.v1.model.ExecuteRequest; 
import com.adobe.target.edge.client.model.TargetDeliveryRequest; 

 
ClientHints clientHints = new ClientHints(); 
clientHints.setMobile(true); 
clientHints.setPlatform("macOS"); 
clientHints.setArchitecture("x86"); 
clientHints.setPlatformVersion("11.3.1"); 
clientHints.setBrowserUAWithMajorVersion( 
  "\" Not A;Brand\";v=\"99\", \"Chromium\";v=\"99\", \"Google Chrome\";v=\"99\""); 
String userAgent = 
  "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Safari/537.36"; 

 
TargetDeliveryRequest request = TargetDeliveryRequest.builder() 
        .execute(new ExecuteRequest().pageLoad(pageLoad)) 
        .context(new Context().clientHints(clientHints).userAgent(userAgent)) 
        .build(); 
```

>[!ENDTABS]

## Apparaatbeslissingen

In de volgende tabel wordt aangegeven welke publieksregels worden ondersteund voor apparaatbeslissingen.

| Auditieregel | Apparaatbeslissingen |
| --- | --- |
| [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Ja |
| [Netwerk](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | Nee |
| [Mobiel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | Nee |
| [Aangepaste parameters](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Ja |
| [Besturingssysteem](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Ja |
| [Sitepagina&#39;s](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Ja |
| [Browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Ja |
| [Bezoekerprofiel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | Nee |
| [verkeersbronnen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | Nee |
| [Tijdschema](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Ja |
| [Experience Cloud publiek](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Soorten publiek uit Adobe Audience Manager, Adobe Analytics en Adobe Experience Manager) | Nee |

### Geo targeting voor apparaatbesluitvorming

Om bijna-nul latentie voor op apparaat beslissingsactiviteiten met op geo-Gebaseerd publiek te handhaven, adviseert Adobe u de geo waarden zelf in de vraag te verstrekken aan `getOffers`. Doe dit door de `Geo` object in het `Context` van het verzoek. Dit betekent dat uw server een manier nodig heeft om de locatie van elke eindgebruiker te bepalen. Bijvoorbeeld, kan uw server een IP-aan-Geo raadpleging uitvoeren, gebruikend de dienst u vormt. Sommige hostingproviders, zoals Google Cloud, bieden deze functionaliteit via aangepaste headers in elk `HttpServletRequest`.

>[!BEGINTABS]

>[!TAB Node.js SDK]

```js {line-numbers="true"}
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

>[!TAB Java SDK]

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

Nochtans, als u niet de capaciteit hebt om IP-aan-Geo raadplegingen op uw server uit te voeren, maar u wilt nog op-apparatenbesluit voor uitvoeren `getOffers` aanvragen die op geo gebaseerde doelgroepen bevatten, wordt dit ook ondersteund. Het nadeel van deze benadering is dat het een verre IP-aan-Geo raadpleging zal gebruiken, die latentie aan elk zal toevoegen `getOffers` vraag. Deze latentie moet lager zijn dan een externe vertraging `getOffers` aanroep, aangezien deze een CDN raakt die zich dicht bij uw server bevindt. U moet **alleen** de `ipAddress` in het veld `Geo` object in het `Context` van uw verzoek, zodat de SDK de geolocatie van het IP-adres van uw gebruiker kan ophalen. Indien een ander veld naast de `ipAddress` wordt verstrekt, [!DNL Target] SDK haalt de metagegevens voor de geolocatie niet op voor oplossing.

>[!BEGINTABS]

>[!TAB Node.js SDK]

```js {line-numbers="true"}
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

>[!TAB Java SDK]

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

## Beslissing op de server

In de volgende tabel wordt aangegeven welke publieksregels worden ondersteund voor beslissingen op de server.

| Auditieregel | Beslissing op de server |
| --- | --- |
| [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Ja |
| [Netwerk](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | Ja |
| [Mobiel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | Ja |
| [Aangepaste parameters](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Ja |
| [Besturingssysteem](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Ja |
| [Sitepagina&#39;s](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Ja |
| [Browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Ja |
| [Bezoekerprofiel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | Ja |
| [verkeersbronnen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | Ja |
| [Tijdschema](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Ja |
| [Experience Cloud publiek](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Soorten publiek uit Adobe Audience Manager, Adobe Analytics en Adobe Experience Manager) | Ja |
