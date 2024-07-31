---
keywords: Overzicht en referentie, webkit, cookies, eerste-partij, derde partij, eerste-partij, derde partij, $8
description: Meer informatie over het gedrag van de cookie van het doel (cookie van de eerste fabrikant, cookie van derden met cookie van de eerste fabrikant of cookie van derden alleen).
title: Waar kan ik informatie over doelcookies vinden?
feature: at.js
role: Developer
source-git-commit: 39f390a0e5eedf8c6957333759d31d96ed11b321
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 0%

---

# Doelcookies

Het gedrag van de cookie hangt af van het feit of het een cookie van een eerste partij, een cookie van een derde partij met een cookie van de eerste partij of van een cookie van een andere fabrikant alleen is.

>[!NOTE]
>
>Dit onderwerp bevat informatie over `mboxSession` en `mboxPC` . Op basis van de best practices voor implementatie wordt aanbevolen geen vertrouwelijke informatie te koppelen of op te slaan met de cookiegegevens: `mboxSession` of `mboxPC` .

Zie ook [ Schrapping het koekje van het Doel ](/help/dev/before-implement/privacy/cookie-deleting.md).

## Wanneer om Eerste of derdekoekjes te gebruiken

De site-instelling bepaalt welke cookies u wilt gebruiken. Het is handig om te begrijpen hoe Target werkt wanneer u probeert cookies van derden en van derden te begrijpen. Zie [ hoe Adobe Target ](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html) voor meer informatie werkt.

Er zijn drie hoofdtoepassingen voor cookies:

1. Eén domein.

   Al uw tests vinden plaats binnen één top-level domein (`www.domain.com`, `store.domain.com`, `anysub.domain.com`, etc.).

   Benadering: alleen cookies van de eerste partij gebruiken (de standaardwaarde).

1. De gebruikers kruisen domeinen en u wilt hun gedrag over deze domeinen volgen en testen.

   Voorbeeld: een gebruiker komt naar uw site om te winkelen, maar checkt dit uit via Yahoo-winkels. Drie benaderingen (werk samen met uw accountvertegenwoordiger om de beste aanpak te bepalen):

   * Cookies van de eerste en derde partij inschakelen.
   * Schakel alleen derden in (zelden, maar heeft het voordeel dat de cookie uit uw domein blijft).
   * Schakel alleen cookies van de eerste partij in en geef de parameter `mboxSession` door wanneer u het domein overschrijdt.

     De parameter `mboxSession` moet worden doorgegeven aan een bestemmingspagina en vanuit de JavaScript-bibliotheek worden benaderd (Adobe Experience Platform Web SDK of at.js). Het kan geen tussenliggende redirector-pagina zijn.

1. U gebruikt alleen adboxes of FlashBox op een externe site.

   Twee benaderingen (werk samen met uw accountvertegenwoordiger om de beste aanpak te bepalen):

   * Cookies van de eerste en derde partij inschakelen.

     Cookies van de eerste en derde partij zijn vereist voor FlashBox en dynamische creatieve producten.

   * Schakel alleen cookies van derden in.

     Deze benadering is slechts voor het zeldzame geval waar implementaties AdBox zonder onsite het richten worden gebruikt.

## Werking cookie eerste partij

Het cookie van de eerste partij wordt opgeslagen in clientdomain.com, waarbij `clientdomain` uw domein is.

De JavaScript-bibliotheek genereert een `mboxSession ID` en slaat deze op in het doelcookie. De eerste mbox-reactie bevat de aanbieding en de JavaScript slaat de `mboxPC ID` die door de toepassing is gegenereerd, op in het mbox-cookie.

>[!NOTE]
>
>Het cookie van AMCV_##@AdobeOrg van de eerste partij wordt altijd ingesteld met de Experience Cloud Bezoeker-id.

## Gedrag cookie van derden

Het cookie van derden wordt opgeslagen in clientcode.tt.omtrdc.net en het cookie van de eerste fabrikant wordt opgeslagen in clientdomain.com, waar `clientdomain` uw domein is.

De JavaScript-bibliotheek genereert een `mboxSession ID` . De eerste locatieaanvraag retourneert HTTP-antwoordheaders die proberen cookies van derden met de naam `mboxSession` en `mboxPC` in te stellen en een omleidingsaanvraag wordt teruggestuurd met een extra parameter ( `mboxXDomainCheck=true` ).

Als de browser cookies van derden accepteert, bevat de omleidingsaanvraag deze cookies en wordt de aanbieding geretourneerd.

Als de browser cookies van derden afwijst, worden deze cookies niet opgenomen in de omleidingsaanvraag en wordt standaardinhoud weergegeven voor alle locaties op de pagina. Omdat er geen cookies zijn ingesteld, vindt hetzelfde proces hierboven opnieuw plaats bij elke paginaaanvraag.

>[!NOTE]
>
>Het cookie demdex.net wordt ingesteld als cookies van derden niet worden geblokkeerd.

## Gedrag cookie van derden en eerste partij

Het cookie van derden wordt opgeslagen in clientcode.tt.omtrdc.net en het cookie van de eerste fabrikant wordt opgeslagen in clientdomain.com, waar `clientdomain` uw domein is.

De JavaScript-bibliotheek genereert een `mboxSession ID` . De eerste plaatsaanvraag retourneert HTTP-antwoordheaders die proberen cookies van derden met de naam `mboxSession` en `mboxPC` in te stellen, en een omleidingsverzoek wordt teruggestuurd met een extra parameter (`mboxXDomainCheck=true`).

Als de browser cookies van derden accepteert, bevat de omleidingsaanvraag deze cookies en wordt de aanbieding geretourneerd.

Sommige browsers wijzen cookies van derden af. Als het cookie van een andere fabrikant wordt geblokkeerd, werkt het cookie van de eerste partij nog steeds. Doel probeert het cookie van derden in te stellen. Als dit niet het geval is, kan Target alleen het specifieke domein van de client bijhouden. Interdomeintracering werkt niet als het cookie van derden wordt geblokkeerd, tenzij `mboxSession` wordt toegevoegd aan de koppeling die domeinen kruist. In dit geval wordt een ander cookie van de eerste fabrikant ingesteld en gesynchroniseerd met het cookie van het vorige domein.

## Cookie-instellingen

Het cookie heeft verschillende standaardinstellingen. U kunt deze instellingen desgewenst wijzigen, met uitzondering van de duur van het cookie. Vraag uw accountvertegenwoordiger wanneer u de cookie-instellingen wijzigt.

| Instelling | Informatie |
|--- |--- |
| Naam cookie | mbox. |
| Cookie-domein | Het tweede en bovenste niveau van de domeinen waaruit u de inhoud aanbiedt. Omdat het van het domein van uw bedrijf wordt gediend, is het koekje een eerste-partijkoekje.<br /> Voorbeeld: `mycompany.com`. |
| Serverdomein | `clientcode.tt.omtrdc.net` , met de clientcode voor uw account. |
| Duur van cookie | Het cookie blijft twee weken na de laatste aanmelding in de browser van de bezoeker staan. U kunt de duur van het cookie niet wijzigen. |
| P3P-beleid | De cookie wordt gepubliceerd met een P3P-beleid, zoals vereist door de standaardinstelling in de meeste browsers. Een P3P-beleid geeft aan welke browser de cookie aanbiedt en hoe de informatie wordt gebruikt. |

Het cookie houdt verschillende waarden bij voor het beheren van de manier waarop bezoekers campagnes ervaren:

| Waarde | Definitie |
|--- |--- |
| sessie-id | Een unieke id voor een gebruikerssessie. Deze id duurt standaard 30 minuten. |
| pc-id | Een halfpermanente id voor de browser van een bezoeker. Laadt 14 dagen. |
| controleren | Een eenvoudige testwaarde die wordt gebruikt om te bepalen of een bezoeker cookies ondersteunt. Stel de instellingen in wanneer een bezoeker een pagina aanvraagt. |
| disable | Stel in of de laadtijd van de bezoeker langer is dan de time-out die is geconfigureerd in het JavaScript-bibliotheekbestand. Deze waarde duurt standaard één uur. |

## Effect op Doel voor Safari-bezoekers als gevolg van wijzigingen in tracking van Apple WebKit

**hoe werkt het volgen van Adobe Target?**

| Cookies | Details |
|--- |--- |
| Domeinen van eerste partij | De standaardimplementatie voor klanten van het Doel. De &quot;mbox&quot;koekjes wordt geplaatst in het domein van de klant. |
| Tekstspatiëring van derden | Tekstspatiëring door derden is belangrijk voor reclame en het richten van gebruiksgevallen in Target en Adobe Audience Manager (AAM). Bij het bijhouden van externe gegevens zijn technieken voor scripts die verwijzen naar andere sites, vereist. Het doel gebruikt twee cookies, &quot;mboxSession&quot; en &quot;mboxPC&quot;, die zijn ingesteld in het `clientcode.tt.omtrd.net` -domein. |

**wat is de benadering van Apple?**

Uit Apple:

&quot;Intelligente preventie van tracering is een nieuwe WebKit-functie die het opsporen van gegevens via andere sites beperkt door cookies en andere websitegegevens verder te beperken.&quot;

&quot;Dit wordt intersite tracering genoemd en het cookie dat door `example-tracker.com` wordt gebruikt, wordt een cookie van een andere fabrikant genoemd. In onze test vonden we populaire websites met meer dan 70 van dergelijke trackers, die allemaal ongemerkt gegevens over gebruikers verzamelen.&quot;

| Benadering | Details |
|--- |--- |
| Intelligente tracering | Voor meer informatie, zie [ Intelligente het Volgen Preventie ](https://webkit.org/blog/7675/intelligent-tracking-prevention/) op de WebKit Open Browser van Source website van de Motor van de Motor van het Web. |
| Cookies | Hoe Safari cookies verwerkt:<ul><li>Cookies van derden die zich niet op een domein bevinden waartoe de gebruiker rechtstreeks toegang heeft, worden nooit opgeslagen. Dit gedrag is niet nieuw. Cookies van andere bedrijven worden al niet ondersteund in Safari.</li><li>Cookies van derden die zijn ingesteld op een domein waartoe de gebruiker rechtstreeks toegang heeft, worden na 24 uur gewist.</li><li>Cookies van de eerste partij worden na 30 dagen gezuiverd als dat domein van de eerste partij als het volgen van gebruikers over plaatsen is geclassificeerd. Deze kwestie zou op grote bedrijven kunnen van toepassing zijn die gebruikers naar verschillende domeinen online verzenden. Apple heeft niet duidelijk gemaakt hoe deze domeinen precies worden geclassificeerd, of hoe een domein kan bepalen of zij als het volgen van gebruikers dwars-plaats zijn geclassificeerd.</li></ul> |
| Machine die leert domeinen te identificeren die naar andere sites verwijzen | Van Apple:<br /> het Leren van de Machine Classifier: Een machine het leren model wordt gebruikt om te classificeren welke hoogste privé gecontroleerde domeinen de gebruiker dwars-plaats kunnen volgen, die op de verzamelde statistieken wordt gebaseerd. Van de diverse verzamelde statistieken, bleken drie vectoren sterk signaal voor classificatie te hebben die op huidige volgende praktijken wordt gebaseerd: subresource onder aantal unieke domeinen, subframe onder aantal unieke domeinen, en aantal unieke domeinen opnieuw gericht aan. Alle gegevens verzamelen en classificeren gebeurt op het apparaat.<br /> Nochtans, als de gebruiker met `example.com` als hoogste domein in wisselwerking staat, die vaak als eerste-partijdomein wordt bedoeld, beschouwt de Intelligente het Volgen Preventie het een signaal dat de gebruiker in de website geinteresseerd is en tijdelijk zijn gedrag aanpast zoals die in deze chronologie wordt getoond:<br /> als de gebruiker met `example.com` de laatste 24 uren interactie had, zijn koekjes beschikbaar wanneer `example.com` een derde is. Op deze manier kunt u zich aanmelden met mijn X-account op Y-aanmeldingsscenario&#39;s.<ul><li>De domeinen die als top-level domein worden bezocht worden niet beïnvloed. Sites zoals bijvoorbeeld OKTA</li><li>Identificeert domeinen die subdomein of subframe zijn van de huidige pagina over meerdere unieke domeinen.</li></ul> |

**hoe wordt de Adobe beïnvloed?**

| Betrokken functionaliteit | Details |
|--- |--- |
| Ondersteuning voor uitschakelen | Wijzigingen in WebKit voor Apple worden afgebroken.<br /> het doel opt-out gebruikt een koekje in het `clientcode.tt.omtrdc.net` domein. Voor meer details, zie [ Privacy ](/help/dev/before-implement/privacy/privacy.md).<br /> het Doel steunt twee opt-outs:<ul><li>Eén per client (de client beheert de koppeling om te weigeren).</li><li>Eén via een Adobe die de gebruiker uit alle functionaliteit van het doel voor alle klanten haalt.</li></ul>Beide methoden gebruiken het cookie van derden. |
| Doelactiviteiten | De klanten kunnen hun [ lengte van het profielleven ](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile-lifetime.html) voor hun rekeningen van het Doel (tot 90 dagen) kiezen. Het probleem is dat als de het profielleven van de rekening langer is dan 30 dagen, en het eerste-partijkoekje wordt gezuiverd omdat het domein van de klant als het volgen van gebruikers dwars-plaats is gemerkt, het gedrag voor bezoekers Safari op de volgende gebieden in Doel wordt beïnvloed:<br />**[!UICONTROL Target reports]**: Als een gebruiker Safari in een activiteit ingaat, na 30 dagen terugkeert, en dan omzet, die gebruiker telt als twee bezoekers en één omzetting.<br /> dit gedrag is het zelfde voor activiteiten die Analytics gebruiken als rapporteringsbron (A4T).<br />**[!UICONTROL Profile & activity membership]**<ul><li>Profielgegevens worden gewist wanneer het cookie van de eerste partij verloopt.</li><li>Het lidmaatschap van de activiteit wordt gewist wanneer het eerste-partijkoekje verloopt.</li><li> Het doel werkt niet in Safari voor accounts die een cookie-implementatie van een andere fabrikant of een cookie-implementatie van een andere fabrikant gebruiken. Dit gedrag is niet nieuw. Safari heeft cookies van derden al een tijdje niet toegestaan.</li></ul><br />**[!UICONTROL Suggestions]**: Als er een zorg is dat het klantendomein als één het volgen bezoekers dwars-zitting zou kunnen worden gemerkt, is het veiligst om het profielleven aan 30 dagen of minder in Doel te plaatsen. Deze limiet zorgt ervoor dat gebruikers op dezelfde manier worden bijgehouden in Safari en alle andere browsers. |
