---
keywords: Overzicht en referentie, webkit, cookies, eerste-partij, derde partij, eerste-partij, derde partij,
description: Meer informatie over [!DNL Target] cookie gedrag (cookie van de eerste gebruiker, cookie van derden met cookie van de eerste gebruiker of cookie van een andere fabrikant alleen).
title: Waar kan ik informatie vinden over [!DNL Target] Cookies?
feature: at.js
exl-id: d44e02ce-8920-4130-bcad-699ca77c0dad
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 0%

---

# [!DNL Target] cookies

Het gedrag van de cookie hangt af van het feit of het een cookie van een eerste partij, een cookie van een derde partij met een cookie van de eerste partij of van een cookie van een andere fabrikant alleen is.

>[!NOTE]
>
>Voor gedetailleerde informatie over de verschillende cookies die worden gebruikt door [!DNL Target], zie [[!DNL Adobe Target] cookies](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-target.html){target=_blank} in de *Experience Cloud Central Interface Components Guide*.
>
>Dit onderwerp bevat informatie over `mboxSession` en `mboxPC`. Op basis van de best practices voor implementatie wordt aanbevolen geen vertrouwelijke informatie te koppelen of op te slaan met de cookiegegevens: `mboxSession` of `mboxPC`.

Zie ook [Verwijder de [!DNL Target] koekje](cookie-deleting.md).

## Wanneer cookies van andere leveranciers of leveranciers gebruiken

De site-instelling bepaalt welke cookies u wilt gebruiken. Het is handig om te begrijpen hoe [!DNL Target] werkt bij het begrijpen van cookies van derden. Zie [Hoe [!DNL Adobe] [!DNL Target] Werken](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html) voor meer informatie .

Er zijn drie hoofdtoepassingen voor cookies:

1. Eén domein.

   Al uw tests vinden plaats binnen één top-level domein (`www.domain.com`, `store.domain.com`, `anysub.domain.com`, enzovoort).

   Benadering: alleen cookies van de eerste partij gebruiken (de standaardwaarde).

1. De gebruikers kruisen domeinen en u wilt hun gedrag over deze domeinen volgen en testen.

   Voorbeeld: een gebruiker komt naar uw site om te winkelen, maar checkt dit uit via Yahoo-winkels. Drie benaderingen (werk samen met uw accountvertegenwoordiger om de beste aanpak te bepalen):

   * Cookies van de eerste en derde partij inschakelen.
   * Schakel alleen derden in (zelden, maar heeft het voordeel dat de cookie uit uw domein blijft).
   * Alleen cookies van eerste partij inschakelen en doorgeven `mboxSession` parameter wanneer het oversteken van domein.

     De `mboxSession` parameter moet worden doorgegeven aan een bestemmingspagina en vanuit de JavaScript-bibliotheek worden benaderd (Adobe Experience Platform Web SDK of at.js). Het kan geen tussenliggende redirector-pagina zijn.

1. U gebruikt alleen adboxes of FlashBox op een externe site.

   Twee benaderingen (werk samen met uw accountvertegenwoordiger om de beste aanpak te bepalen):

   * Cookies van de eerste en derde partij inschakelen.

     Cookies van de eerste en derde partij zijn vereist voor FlashBox en dynamische creatieve producten.

   * Schakel alleen cookies van derden in.

     Deze benadering is slechts voor het zeldzame geval waar implementaties AdBox zonder onsite het richten worden gebruikt.

## Cookie-gedrag van de eerste partij

Het cookie van de eerste partij wordt opgeslagen in clientdomain.com, waar `clientdomain` is uw domein.

De JavaScript-bibliotheek genereert een `mboxSession ID` en slaat het op in het [!DNL Target] cookie. De eerste mbox-reactie bevat de aanbieding en de JavaScript-code waarin de `mboxPC ID` gegenereerd door de toepassing, in het mbox-cookie.

>[!NOTE]
>
>Het cookie van AMCV_##@AdobeOrg van de eerste partij wordt altijd ingesteld met de Experience Cloud-bezoeker-id.

## Cookie-gedrag van derden

Het cookie van derden wordt opgeslagen in clientcode.tt.omtrdc.net en het cookie van de eerste fabrikant wordt opgeslagen in clientdomain.com, waar `clientdomain` is uw domein.

De JavaScript-bibliotheek genereert een `mboxSession ID`. De eerste locatieaanvraag retourneert HTTP-antwoordheaders die proberen cookies van derden met een naam in te stellen `mboxSession` en `mboxPC` en een omleidingsverzoek wordt teruggestuurd met een extra parameter ( `mboxXDomainCheck=true`).

Als de browser cookies van derden accepteert, bevat de omleidingsaanvraag deze cookies en wordt de aanbieding geretourneerd.

Als de browser cookies van derden afwijst, worden deze cookies niet opgenomen in de omleidingsaanvraag en wordt standaardinhoud weergegeven voor alle locaties op de pagina. Omdat er geen cookies zijn ingesteld, vindt hetzelfde proces hierboven opnieuw plaats bij elke paginaaanvraag.

>[!NOTE]
>
>Het cookie demdex.net wordt ingesteld als cookies van derden niet worden geblokkeerd.

## Cookie-gedrag van derden en van derden

Het cookie van derden wordt opgeslagen in clientcode.tt.omtrdc.net en het cookie van de eerste fabrikant wordt opgeslagen in clientdomain.com, waar `clientdomain` is uw domein.

De JavaScript-bibliotheek genereert een `mboxSession ID`. De eerste locatieaanvraag retourneert HTTP-antwoordheaders die proberen cookies van derden met een naam in te stellen `mboxSession` en `mboxPC`en er wordt een omleidingsverzoek teruggestuurd met een extra parameter (`mboxXDomainCheck=true`).

Als de browser cookies van derden accepteert, bevat de omleidingsaanvraag deze cookies en wordt de aanbieding geretourneerd.

Sommige browsers wijzen cookies van derden af. Als het cookie van een andere fabrikant wordt geblokkeerd, werkt het cookie van de eerste partij nog steeds. [!DNL Target] pogingen om het cookie van derden in te stellen, en als dit niet het geval is, dan [!DNL Target] kan alleen het specifieke domein van de client bijhouden. Interdomeintracering werkt niet als het cookie van een andere fabrikant wordt geblokkeerd, tenzij de methode `mboxSession` wordt toegevoegd in de verbinding die domeinen kruist. In dit geval wordt een ander cookie van de eerste fabrikant ingesteld en gesynchroniseerd met het cookie van het vorige domein.

## Cookie-instellingen

Het cookie heeft verschillende standaardinstellingen. U kunt deze instellingen desgewenst wijzigen, met uitzondering van de duur van het cookie. Vraag uw accountvertegenwoordiger wanneer u de cookie-instellingen wijzigt.

| Instelling | Informatie |
|--- |--- |
| Naam cookie | mbox. |
| Cookie-domein | Het tweede en bovenste niveau van de domeinen waaruit u de inhoud aanbiedt. Omdat het van het domein van uw bedrijf wordt gediend, is het koekje een eerste-partijkoekje.<br />Voorbeeld: `mycompany.com`. |
| Serverdomein | `clientcode.tt.omtrdc.net`, met de clientcode voor uw account. |
| Duur van cookie | Het cookie blijft twee weken na de laatste aanmelding in de browser van de bezoeker staan. U kunt de duur van het cookie niet wijzigen. |
| P3P-beleid | De cookie wordt gepubliceerd met een P3P-beleid, zoals vereist door de standaardinstelling in de meeste browsers. Een P3P-beleid geeft aan welke browser de cookie aanbiedt en hoe de informatie wordt gebruikt. |

Het cookie houdt verschillende waarden bij voor het beheren van de manier waarop bezoekers campagnes ervaren:

| Waarde | Definitie |
|--- |--- |
| sessie-id | Een unieke id voor een gebruikerssessie. Deze id duurt standaard 30 minuten. |
| pc-id | Een halfpermanente id voor de browser van een bezoeker. Laadt 14 dagen. |
| controleren | Een eenvoudige testwaarde die wordt gebruikt om te bepalen of een bezoeker cookies ondersteunt. Stel de instellingen in wanneer een bezoeker een pagina aanvraagt. |
| disable | Stel in of de laadtijd van de bezoeker langer is dan de time-out die is geconfigureerd in het JavaScript-bibliotheekbestand. Deze waarde duurt standaard één uur. |

## Gevolgen voor [!DNL Target] voor Safari-bezoekers vanwege wijzigingen in het bijhouden van Apple WebKit

**Hoe werkt [!DNL Target] volgen, werk?**

| Cookies | Details |
|--- |--- |
| Domeinen van eerste partij | De standaardimplementatie voor [!DNL Target] klanten. De &quot;mbox&quot;koekjes wordt geplaatst in het domein van de klant. |
| Tekstspatiëring van derden | Tekstspatiëring door derden is belangrijk voor reclame en doelgericht gebruik in gevallen waarin [!DNL Target] en in [!DNL Adobe Audience Manager] (AAM) Bij het bijhouden van externe gegevens zijn technieken voor scripts die verwijzen naar andere sites, vereist. [!DNL Target] gebruikt twee cookies, &quot;mboxSession&quot; en &quot;mboxPC&quot; ingesteld in het dialoogvenster `clientcode.tt.omtrd.net` domein. |
**Wat is de aanpak van Apple?**

Uit Apple:

&quot;Intelligente preventie van tracering is een nieuwe WebKit-functie die het opsporen van gegevens via andere sites beperkt door cookies en andere websitegegevens verder te beperken.&quot;

&quot;Dit wordt intersite tracering genoemd en het cookie dat wordt gebruikt door `example-tracker.com` wordt een cookie van een andere fabrikant genoemd. In onze test vonden we populaire websites met meer dan 70 van dergelijke trackers, die allemaal ongemerkt gegevens over gebruikers verzamelen.&quot;

| Benadering | Details |
|--- |--- |
| Intelligente tracering | Zie voor meer informatie [Intelligente traceringspreventie](https://webkit.org/blog/7675/intelligent-tracking-prevention/) op de WebKit Open Source Web Browser Engine website. |
| Cookies | Hoe Safari cookies verwerkt:<ul><li>Cookies van derden die zich niet op een domein bevinden waartoe de gebruiker rechtstreeks toegang heeft, worden nooit opgeslagen. Dit gedrag is niet nieuw. Cookies van andere bedrijven worden al niet ondersteund in Safari.</li><li>Cookies van derden die zijn ingesteld op een domein waartoe de gebruiker rechtstreeks toegang heeft, worden na 24 uur gewist.</li><li>Cookies van de eerste partij worden na 30 dagen gezuiverd als dat domein van de eerste partij als het volgen van gebruikers over plaatsen is geclassificeerd. Deze kwestie zou op grote bedrijven kunnen van toepassing zijn die gebruikers naar verschillende domeinen online verzenden. Apple heeft niet duidelijk gemaakt hoe deze domeinen precies worden geclassificeerd, of hoe een domein kan bepalen of zij als het volgen van gebruikers dwars-plaats zijn geclassificeerd.</li></ul> |
| Machine die leert domeinen te identificeren die naar andere sites verwijzen | Uit Apple:<br />Machine Learning Classifier: Een machine-leermodel wordt gebruikt om te classificeren welke hoogste privé gecontroleerde domeinen de gebruiker dwars-plaats kunnen volgen, die op de verzamelde statistieken wordt gebaseerd. Van de diverse verzamelde statistieken, bleken drie vectoren sterk signaal voor classificatie te hebben die op huidige volgende praktijken wordt gebaseerd: subresource onder aantal unieke domeinen, subframe onder aantal unieke domeinen, en aantal unieke domeinen opnieuw gericht aan. Alle gegevens verzamelen en classificeren gebeurt op het apparaat.<br />Als de gebruiker echter met `example.com` Als het bovenste domein, dat vaak als een domein van de eerste partij wordt bedoeld, beschouwt de Intelligente het Volgen Preventie het een signaal dat de gebruiker in de website geinteresseerd is en tijdelijk zijn gedrag zoals die in deze chronologie wordt getoond aanpast:<br />Als de gebruiker interactie had met `example.com` in de laatste 24 uur zijn de cookies ervan beschikbaar wanneer `example.com` is een derde. Op deze manier kunt u zich aanmelden met mijn X-account op Y-aanmeldingsscenario&#39;s.<ul><li>De domeinen die als top-level domein worden bezocht worden niet beïnvloed. Sites zoals bijvoorbeeld OKTA</li><li>Identificeert domeinen die subdomein of subframe zijn van de huidige pagina over meerdere unieke domeinen.</li></ul> |

**Hoe wordt [!DNL Adobe] getroffen?**

| Betrokken functionaliteit | Details |
|--- |--- |
| Ondersteuning voor uitschakelen | Wijzigingen in WebKit voor Apple worden afgebroken.<br />De optie voor het niet volgen van doelen gebruikt een cookie in het dialoogvenster `clientcode.tt.omtrdc.net` domein. Zie voor meer informatie [Privacy](privacy.md).<br />Doel ondersteunt twee opt-outs:<ul><li>Eén per client (de client beheert de koppeling om te weigeren).</li><li>Eén via [!DNL Adobe] dat de gebruiker uit alle [!DNL Target] functionaliteit voor alle klanten.</li></ul>Beide methoden gebruiken het cookie van derden. |
| Doelactiviteiten | Klanten kunnen hun [lengte van profielleven](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile-lifetime.html) voor hun [!DNL Target] accounts (maximaal 90 dagen). Het probleem is dat als de profiellevensduur van de account langer is dan 30 dagen en de cookie van de eerste partij wordt gewist omdat het domein van de klant is gemarkeerd als het controleren van gebruikers naar andere sites, het gedrag voor Safari-bezoekers wordt beïnvloed in de volgende gebieden in Target:<br />**Doelrapporten**: Als een gebruiker Safari een activiteit ingaat, na 30 dagen terugkeert, en dan omzet, telt die gebruiker als twee bezoekers en één omzetting.<br />Dit gedrag is het zelfde voor activiteiten die Analytics gebruiken zoals de rapporteringsbron (A4T).<br />**Profiel en lidmaatschap van activiteiten**:<ul><li>Profielgegevens worden gewist wanneer het cookie van de eerste partij verloopt.</li><li>Het lidmaatschap van de activiteit wordt gewist wanneer het eerste-partijkoekje verloopt.</li><li> [!DNL Target] werkt niet in Safari voor accounts die een cookie-implementatie van een andere fabrikant of een cookie-implementatie van een andere fabrikant gebruiken. Dit gedrag is niet nieuw. Safari heeft cookies van derden al een tijdje niet toegestaan.</li></ul><br />**Suggesties**: Als er een zorg is dat het klantendomein als één het volgen bezoekers dwars-zitting zou kunnen worden gemerkt, is het het veiligst om het profielleven aan 30 dagen of minder in Doel te plaatsen. Deze limiet zorgt ervoor dat gebruikers op dezelfde manier worden bijgehouden in Safari en alle andere browsers. |
