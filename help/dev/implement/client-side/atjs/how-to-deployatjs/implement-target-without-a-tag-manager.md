---
keywords: doel, implementatie, implementatie, implementatie van at.js, tagbeheer, apparaatbeslissingen implementeren
description: Leer hoe u de instellingen opgeeft (accountgegevens, implementatiemethoden, enz.) om de [!DNL Adobe Target] bibliotheek at.js zonder een tagbeheer te gebruiken.
title: Kan ik implementeren [!DNL Target] zonder tagbeheer?
feature: Implement Server-side
exl-id: f675ae21-105d-4aa3-9926-59291f1136b5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1709'
ht-degree: 3%

---

# Implementeren [!DNL Target] zonder tagbeheer

Informatie over de uitvoering [!DNL Adobe Target] zonder gebruik te maken van tagbeheer of tags in [!DNL Adobe Experience Platform].

>[!NOTE]
>
>Tags in [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) de voorkeursmethode voor de implementatie [!DNL Target] en de bibliotheek at.js. De volgende informatie is niet van toepassing wanneer u tags gebruikt in [!DNL Adobe Experience Platform] uitvoeren [!DNL Target].

Als u de pagina Implementatie wilt openen, klikt u **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

U kunt de volgende instellingen opgeven op deze pagina:

* Accountgegevens
* Implementatiemethoden
* Profile API
* Foutopsporingsgereedschappen
* Privacy

>[!NOTE]
>
>U kunt instellingen in de bibliotheek at.js overschrijven in plaats van ze te configureren in het dialoogvenster [!DNL Target] Standaard/Premium-gebruikersinterface of met REST-API&#39;s. Zie voor meer informatie [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

## Accountgegevens

U kunt de volgende accountdetails weergeven. Deze instellingen kunnen niet worden gewijzigd.

| Instelling | Beschrijving |
| --- | --- |
| [!UICONTROL Client Code] | De clientcode is een client-specifieke reeks tekens die vaak vereist zijn bij het gebruik van de [!DNL Target] API&#39;s. |
| [!UICONTROL IMS Organization ID] | Deze id koppelt uw implementatie aan uw Adobe Experience Cloud-account. |
| [!UICONTROL On-Device Decisioning] | Schuif de schakeloptie naar de stand &quot;aan&quot; om de apparaatbesturing in te schakelen.<p>Door op het apparaat te beslissen kunt u uw A/B- en Experience Targeting (XT)-campagnes op uw server in het cachegeheugen plaatsen en in het geheugen beslissen bij bijna-nullatentie. Zie voor meer informatie [Inleiding tot apparaatbeslissingen](../../../server-side/sdk-guides/on-device-decisioning/overview.md). |
| [!UICONTROL Include all existing on-device decisioning qualified activities in the artifact] | (Voorwaardelijk) Deze optie wordt weergegeven als u het bepalen op het apparaat inschakelt.<p>Sleep de schakeloptie naar de positie &quot;Aan&quot; als u al uw live wilt [!DNL Target] activiteiten die in aanmerking komen voor beslissingen op het apparaat moeten automatisch in het artefact worden opgenomen.<p>Als u deze schakeloptie uitschakelt, moet u alle beslissingsactiviteiten op het apparaat opnieuw maken en activeren, zodat deze worden opgenomen in het gegenereerde regelartefact. |

## Implementatiemethoden

U kunt de volgende instellingen configureren in het deelvenster Implementatiemethoden:

### Algemene instellingen

>[!NOTE]
>
>Deze instellingen worden toegepast op alle [!DNL Target] .js-bibliotheken. Nadat u wijzigingen hebt aangebracht in de sectie Implementatiemethoden, moet u de bibliotheek downloaden en bijwerken in uw implementatie.

| Instelling | Beschrijving |
| --- | --- |
| [!UICONTROL Page load enabled (Auto-create global mbox)] | Geef op of u de algemene mbox-aanroep in het bestand at.js wilt insluiten om automatisch op elke pagina te starten. |
| [!UICONTROL Global mbox] | Selecteer een naam voor het globale vakje. Deze naam is standaard target-global-mbox.<p>Speciale tekens, zoals ampersands (&amp;), kunnen worden gebruikt in mbox-namen met at.js. |
| [!UICONTROL Timeout (seconds)] | Indien [!DNL Target] reageert niet met inhoud binnen de gedefinieerde periode, de wachttijden van de serveraanroep zijn verstreken en de standaardinhoud wordt weergegeven. Aanvullende aanroepen worden nog steeds geprobeerd tijdens de sessie van de bezoeker. De standaardwaarde is 5 seconden.<p>De bibliotheek at.js gebruikt de time-outinstelling in `XMLHttpRequest`. De time-out begint wanneer de aanvraag wordt geactiveerd en stopt wanneer [!DNL Target] krijgt een reactie van de server. Zie voor meer informatie [XMLHttpRequest.timeout](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/timeout) op het Mozilla Developer Network.<p>Als de opgegeven time-out optreedt voordat de reactie wordt ontvangen, wordt standaardinhoud weergegeven en wordt de bezoeker wellicht geteld als een deelnemer aan een activiteit omdat alle gegevensverzameling plaatsvindt op het tabblad [!DNL Target] rand. Als de aanvraag de [!DNL Target] edge, de bezoeker wordt geteld.<p>Denk aan het volgende wanneer u de time-outinstelling configureert:<ul><li>Als de waarde te laag is, kunnen gebruikers de standaardinhoud het grootste deel van de tijd zien, hoewel de bezoeker als deelnemer aan de activiteit kon worden geteld.</li><li>Als de waarde te hoog is, kunnen bezoekers lege gebieden op uw webpagina of lege pagina&#39;s zien als u de hoofdtekst gedurende langere perioden verbergt.</li></ul>Om een beter inzicht in mbox reactietijden te krijgen, bekijk het lusje van het Netwerk in de Hulpmiddelen van de Ontwikkelaar van uw browser. U kunt ook controlehulpmiddelen voor webprestaties van derden gebruiken, zoals Catchpoint.<p>**Opmerking**: De [bezoekerApiTimeout](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#visitorapitimeout) het plaatsen zorgt ervoor dat [!DNL Target] wacht niet te lang op de reactie van de bezoeker-API. Deze instelling en de instelling Time-out voor at.js die hier wordt beschreven, zijn niet van invloed op elkaar. |
| [!UICONTROL Profile Lifetime] | Deze instelling bepaalt hoe lang bezoekersprofielen worden opgeslagen. Profielen worden standaard twee weken opgeslagen. Deze instelling kan tot 90 dagen worden verhoogd.<p>Neem contact op met [Clientservice](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html#reference_ACA3391A00EF467B87930A450050077C). |

### Hoofduitvoeringsmethode

>[!NOTE]
>
>[!DNL Adobe Target]  ondersteunt beide at.js 1.*x* en te.js 2.*x*. Voer een upgrade uit naar de meest recente update van een van de belangrijkste versies van at.js om ervoor te zorgen dat u een ondersteunde versie uitvoert.

Klik op de betreffende toepassing om de gewenste versie van at.js te downloaden. **Downloaden** knop.

Als u de instelling at.js wilt bewerken, klikt u op **[!UICONTROL Edit]** naast de gewenste versie at.js.

>[!WARNING]
>
>Voordat u deze standaardinstellingen wijzigt, moet u eerst contact opnemen met [Clientservice](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html#reference_ACA3391A00EF467B87930A450050077C) dus u heeft geen invloed op uw huidige implementatie.

Naast de hierboven beschreven instellingen zijn ook de volgende specifieke instellingen van at.js beschikbaar:

| Instelling | Beschrijving |
|--- |--- |
| Domeinoverschrijdend | Voor at.js v1.*x*, specificeer of de dwars-domeinmogelijkheden zijn `disabled` (browsers stellen alleen cookies in uw domein in (cookies van de eerste partij), `x only` (browsers stellen cookies alleen in het domein van Target in) of beide door `enabled` (browsers stellen cookies van zowel de eerste als de derde partij in). Geef voor at.js v2.10 en hoger op of de mogelijkheden voor verschillende domeinen `enabled` (browsers stellen cookies van zowel de 1e als de 3de partij in) of `disabled` (browsers kunnen cookies van derden niet instellen). |
| Aangepaste bibliotheekkop | Voeg aangepaste JavaScript toe die u boven aan de bibliotheek wilt opnemen. |
| Aangepaste bibliotheekvoettekst | Voeg aangepaste JavaScript toe die u onder aan de bibliotheek wilt opnemen. |

### Profile API

Schakel verificatie voor batchupdates via API in of uit en genereer een profielverificatietoken.

Zie voor meer informatie [Profiel-API-instellingen](/help/dev/before-implement/methods-to-get-data-into-target/profile-api-settings.md).

### Foutopsporingsgereedschappen

Genereer een machtigingstoken voor geavanceerd gebruik [!DNL Target] foutopsporingsgereedschappen. Klik op **[!UICONTROL Generate New Authentication Token]**.

![Nieuwe verificatietoken genereren](../../../../before-implement/methods-to-get-data-into-target/assets/debugger-auth-token.png)

### Privacy

Met deze instellingen kunt u [!DNL Target] in overeenstemming met de toepasselijke wetgeving inzake gegevensbescherming.

Kies het gewenste plaatsen van de IP van de Bezoeker van de Verduistering adresdrop-down lijst:

* Recentste octet-verduistering
* Volledige IP-verduistering
* Geen

Zie voor meer informatie [Privacy](/help/dev/before-implement/privacy/privacy.md).

>[!NOTE]
>
>De optie Verouderde browserondersteuning was beschikbaar in versie 0.js 0.9.3 en eerder. Deze optie is verwijderd in versie 0.js 0.9.4. Voor een lijst met browsers die door at.js worden ondersteund, raadpleegt u [Ondersteunde browsers](/help/dev/before-implement/supported-browsers.md).<p>Verouderde browsers zijn oudere browsers die geen volledige ondersteuning bieden voor CORS (Cross Origin Resource Sharing). Deze browsers zijn onder andere: Internet Explorer-browsers ouder dan versie 11 en Safari-versies 6 en lager. Als ondersteuning voor oudere browsers is uitgeschakeld, [!DNL Target] heeft geen inhoud geleverd of bezoekers geteld in rapporten over deze browsers. Als deze optie is ingeschakeld, wordt u aangeraden kwaliteitsborging toe te passen in alle oudere browsers, zodat de klant er optimaal van profiteert.

## Downloaden om.js

Instructies om de bibliotheek te downloaden met de [!DNL Target] of de Download API.

>[!NOTE]
>
>[Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) is de voorkeursmethode voor de implementatie [!DNL Target] en de bibliotheek at.js. De volgende informatie is niet van toepassing wanneer u tags gebruikt in [!DNL Adobe Experience Platform] uitvoeren [!DNL Target].
>
>[!DNL Adobe Target] ondersteunt beide at.js 1.*x* en te.js 2.*x*. Voer een upgrade uit naar de meest recente update van een van de belangrijkste versies van at.js om ervoor te zorgen dat u een ondersteunde versie uitvoert. Voor meer informatie over wat in elke versie is, zie [at.js - Versiedetails](/help/dev/implement/client-side/atjs/target-atjs-versions.md).

### Download om.js met de [!DNL Target] interface

Om te downloaden om.js van [!DNL Target] interface:

1. Klik op **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.
1. Klik in het gedeelte Implementatiemethoden op de knop **[!UICONTROL Download]** naast de gewenste versie at.js.

### Download om.js met de [!DNL Target] API downloaden

Om te downloaden at.js gebruikend API.

1. Haal uw clientcode op.

   Uw clientcode is beschikbaar boven aan het dialoogvenster **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** pagina van de [!DNL Target] interface.

1. Haal uw beheerdersnummer op.

   Deze URL laden:

   ```
   https://admin.testandtarget.omniture.com/rest/v1/endpoint/<varname>client code</varname>
   ```

   Vervangen `client code` met de clientcode uit stap 1.

   Het resultaat van het laden van deze URL moet er ongeveer als volgt uitzien:

   ```
   { 
     "api": "https://admin6.testandtarget.omniture.com/admin/rest/v1" 
   }
   ```

   In dit voorbeeld is &#39;6&#39; het beheerdersnummer.

1. Download om.js.

   Laad deze URL met de volgende structuur. Wanneer u deze URL laadt, wordt het aangepaste bestand at.js gedownload.

   ```
   https://admin<varname>admin number</varname>.testandtarget.omniture.com/admin/rest/v1/libraries/atjs/download?client=<varname>client code</varname>&version=<version number>
   ```

   * Vervangen `admin number` met uw beheerdersnummer.
   * Vervangen `client code` met de clientcode uit stap 1.
   * Vervangen `version number` met het gewenste at.js versienummer (bijvoorbeeld 2.2).

>[!WARNING]
>
>De [!DNL Target] team handhaaft slechts twee versies van at.js-de huidige versie en de tweede-recentste versie. Voer zonodig een upgrade uit om .js om er zeker van te zijn dat u een ondersteunde versie gebruikt. Voor meer informatie over wat in elke versie is, zie [at.js - Versiedetails](/help/dev/implement/client-side/atjs/target-atjs-versions.md).

## at.js-implementatie

te.js moet worden geïmplementeerd in de `<head>` element van elke pagina van uw website.

Een typische implementatie van [!DNL Target] geen tagbeheer, zoals tags in [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) ziet er als volgt uit:

```
<!doctype html> 
<html> 
<head> 
    <meta charset="utf-8"> 
    <title>Title of the Page</title> 
    <!--Preconnect and DNS-Prefetch to improve page load time--> 
    <link rel="preconnect" href="//<client code>.tt.omtrdc.net"> 
    <link rel="dns-prefetch" href="//<client code>.tt.omtrdc.net"> 
    <!--/Preconnect and DNS-Prefetch--> 
    <!--Data Layer to enable rich data collection and targeting--> 
    <script> 
        var digitalData = { 
            "page": { 
                "pageInfo": { 
                    "pageName": "Home" 
                } 
            } 
        }; 
    </script> 
    <!--/Data Layer--> 
    <!-- targetPageParams(), targetPageParamsAll(), Data Providers or targetGlobalSettings() functions to enrich the visitor profile or modify the library settings--> 
    <script> 
        targetPageParams = function() { 
            return { 
                "a": 1, 
                "b": 2, 
                "pageName": digitalData.page.pageInfo.pageName, 
                "profile": { 
                    "age": 26, 
                    "country": { 
                        "city": "San Francisco" 
                    } 
                } 
            }; 
        }; 
    </script> 
    <!--/targetPageParams()--> 
 
    <!--jQuery or other helper libraries should be implemented before at.js if you would like to use their methods in Target--> 
    <script src="jquery-3.3.1.min.js"></script> 
    <!--/jQuery--> 
    <!--Target's JavaScript SDK, at.js--> 
    <script src="at.js"></script> 
    <!--/at.js--> 
</head>
<body> 
    The default content of the page 
</body> 
</html>
```

Houd rekening met de volgende belangrijke opmerkingen:

* Het HTML5 Doctype (bijvoorbeeld `<!doctype html>`) moet worden gebruikt. Niet-ondersteunde of oudere documenttypen kunnen [!DNL Target] kan geen verzoek indienen.
* De opties Preconnect en Prefetch zijn opties die u kunnen helpen uw webpagina&#39;s sneller te laden. Als u deze configuraties gebruikt, zorg ervoor dat u vervangt `<client code>` met uw eigen clientcode, die u kunt verkrijgen via de **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** pagina.
* Als u een gegevenslaag hebt, kunt u het beste zo veel mogelijk definiëren in het dialoogvenster `<head>` van uw pagina&#39;s voordat om.js wordt geladen. Deze plaatsing biedt de maximale mogelijkheid om deze informatie te gebruiken in [!DNL Target] voor personalisatie.
* Speciaal [!DNL Target] functies, zoals `targetPageParams()`, `targetPageParamsAll()`, gegevensleveranciers, en `targetGlobalSettings()` moet worden gedefinieerd na de gegevenslaag en voordat at.js wordt geladen. U kunt deze functies ook opslaan in de sectie Bibliotheekkoptekst van de pagina Bewerken op .js Settings en opslaan als onderdeel van de bibliotheek at.js zelf. Zie voor meer informatie over deze functies [at.js-functies](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md).
* Als u JavaScript-hulplijnbibliotheken gebruikt, zoals jQuery, moet u deze eerst opnemen [!DNL Target] zodat u hun syntaxis en methodes bij het bouwen kunt gebruiken [!DNL Target] ervaringen.
* Omvat om.js in `<head>` van uw pagina&#39;s.

## Omzettingen bijhouden

In het vak Bevestiging van bestelling worden gegevens over bestellingen op uw site vastgelegd en wordt rapportage op basis van inkomsten en bestellingen toegestaan. Met het selectievakje Order Confirmation (Bevestiging bestellen) kunt u ook aanbevelingen uitvoeren, zoals &quot;People that purchase product x also purchase product y.&quot; (Personen die het product hebben gekocht).

>[!NOTE]
>
>Als gebruikers aankopen doen op uw website, raadt Adobe u aan een bevestigingsvak voor bestellingen te implementeren, zelfs als u Analytics gebruikt voor [!DNL Target] (A4T) voor uw rapportage.

1. Voeg op de pagina met orderdetails het mbox-script in volgens het onderstaande model.
1. Vervang de WOORDEN IN KAPITAALLETTERS door dynamische of statische waarden uit de catalogus.

   >[!TIP]
   >
   >U kunt ook ordergegevens in een willekeurige box doorgeven (er hoeft geen naam aan te worden gegeven) `orderConfirmPage`). U kunt ook ordergegevens in meerdere vakken in dezelfde campagne doorgeven.

   ```
   <script type="text/javascript"> 
   adobe.target.trackEvent({ 
       "mbox": "orderConfirmPage", 
       "params":{  
           "orderId": "ORDER ID FROM YOUR ORDER PAGE",  
           "orderTotal": "ORDER TOTAL FROM YOUR ORDER PAGE",  
           "productPurchasedId": "PRODUCT ID FROM YOUR ORDER PAGE, PRODUCT ID2, PRODUCT ID3"  
       } 
   }); 
   </script> 
   ```

>[!NOTE]
>
>Gebruik in het vak Bevestiging bestelling een komma als scheidingsteken om meerdere product-id&#39;s van elkaar te scheiden.

In het bevestigingsvak Volgorde worden de volgende parameters gebruikt:

| Parameter | Beschrijving |
|--- |--- |
| orderId | Unieke waarde om een order voor het tellen van conversies te identificeren.<p>De `orderId` moet uniek zijn. Dubbele orders worden genegeerd in rapporten. |
| orderTotal | Monetaire waarde van de aankoop.<p>Geef het valutasymbool niet door. Gebruik een decimaalteken (geen komma) om decimale waarden aan te geven. |
| productPurchasedId (optioneel) | Door komma&#39;s gescheiden lijst met product-id&#39;s die in de order zijn aangeschaft.<p>Deze product-id&#39;s worden in het auditrapport weergegeven ter ondersteuning van aanvullende rapportanalyse. |
