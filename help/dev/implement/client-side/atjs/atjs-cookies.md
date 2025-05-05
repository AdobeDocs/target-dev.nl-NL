---
keywords: at.js, 2.0, 1.x, cookies
description: Details over hoe [!DNL Adobe Target] at.js 2.x en at.js 1.x verwerken cookies
title: at.js Cookies
feature: at.js
exl-id: 154a844a-6855-4af7-8aed-0719b4c389f5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1711'
ht-degree: 0%

---

# at.js, cookies

Informatie over at.js 2.x en at.js 1.*x* cookie gedrag.

## at.js 2.x, gedrag voor cookie

Voor versie 2.x van at.js (tot, maar niet inclusief, versie 2.10.0), *alleen cookies van de eerste fabrikant worden ondersteund*. Net als in om.js 1.*x*, wordt het cookie van de eerste partij, &quot;mbox,&quot; opgeslagen in `clientdomain.com`, waarbij `clientdomain` is uw domein.

at.js produceert een zitting - identiteitskaart en slaat het in het koekje op. De eerste reactie bevat alle informatie over de activiteit en de `TNT` of `PC ID` door de [!DNL Target] servers. om.js schrijft dan `TNT/PC ID` naar de cookie.

De `AMCV_###@AdobeOrg` first-party cookie wordt altijd ingesteld door de Experience Cloud ID Service, hoewel de `ECID` wordt doorgegeven in [!DNL Target] verzoeken.

>[!NOTE]
>
>Voor versies 2.10.0 en hoger op at.js worden cookies van beide partijen en cookies van andere domeinen ondersteund.

### Ondersteuning voor cookies van derden en voor interdomeintracering

Met interdomeintracering kunt u sessies op twee verwante sites, maar met verschillende domeinen, als één sessie bekijken. U kunt een [!DNL Target] activiteit die zich uitstrekt `siteA.com` en `siteB.com` en de bezoeker zou in de zelfde ervaring blijven wanneer zij domeinen kruisen. Deze functionaliteit is gebonden aan at.js 1.*x* cookie van derden en van derden.

>[!NOTE]
>
>Voor at.js versie 2.10.0 en hoger worden cookies van andere leveranciers en interdomeintracering ondersteund.


## te.js 1.*x* cookie, gedrag

Voor at.js versies 1.*x*, is het gedrag van de cookie afhankelijk van het feit of het een cookie van de eerste fabrikant, een cookie van een derde partij met een cookie van de eerste partij of alleen een cookie van een derde partij is.

### Wanneer cookies van andere leveranciers of leveranciers gebruiken

De site-instelling bepaalt welke cookies u wilt gebruiken. Het is handig om te begrijpen hoe [!DNL Target] werkt bij het begrijpen van cookies van derden. Zie [Hoe [!DNL Adobe Target] werken](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html?lang=nl-NL) voor meer informatie .

Er zijn drie hoofdtoepassingen voor cookies:

1. Eén domein.

   Al uw tests vinden plaats binnen één top-level domein (`www.domain.com`, `store.domain.com`, `anysub.domain.com`, enz.).

   Gebruik alleen cookies van de eerste fabrikant. Dit is de standaardinstelling.

1. De gebruikers kruisen domeinen en u wilt hun gedrag over deze domeinen volgen en testen.

   Voorbeeld: een gebruiker komt naar uw site om te winkelen, maar checkt dit uit via Yahoo-winkels. Drie benaderingen (werk samen met uw accountvertegenwoordiger om de beste aanpak te bepalen):

   * Cookies van de eerste en derde partij inschakelen.
   * Schakel alleen derden in (zeer zelden, maar heeft het voordeel dat u het cookie at.js buiten uw domein houdt).
   * Alleen cookies van eerste partij inschakelen en doorgeven `mboxSession` parameter wanneer het oversteken van domein.

     De `mboxSession` parameter moet worden doorgegeven aan een bestemmingspagina met de verwijzing at.js. Het kan geen tussenliggende redirector-pagina zijn.

1. U gebruikt alleen adboxes of FlashBox op een externe site.

   Twee benaderingen (werk met uw manager van de cliëntdiensten om de beste benadering te bepalen):

   * Cookies van eerste en van derden inschakelen.

     Cookies van de eerste en van derden zijn vereist voor FlashBox en dynamische creatieve producten.

   * Schakel alleen cookies van derden in.

     Deze aanpak geldt alleen in het zeldzame geval waarin adBox-implementaties worden gebruikt zonder dat er een onsite doelversie van de implementaties wordt gemaakt.

### Cookie-gedrag van de eerste partij

Het cookie van de eerste partij wordt opgeslagen in `clientdomain.com`, waarbij `clientdomain` is uw domein.

at.js genereert een `mboxSession ID` en slaat het op in het cookie. De eerste reactie bevat de aanbieding en de JavaScript-code om de `mboxPC ID` gegenereerd door de toepassing, in het cookie.

>[!NOTE]
>
>De `AMCV_###@AdobeOrg` cookie van de eerste partij wordt altijd ingesteld met de Experience Cloud Visitor-id.

### Cookie-gedrag van derden

Het cookie van de andere fabrikant wordt opgeslagen in `clientcode.tt.omtrdc.net` en de cookie van de eerste partij wordt opgeslagen in `clientdomain.com`, waarbij `clientdomain` is uw domein.

at.js genereert een `mboxSession ID`. De eerste locatieaanvraag retourneert HTTP-antwoordheaders die proberen cookies van derden met een naam in te stellen `mboxSession` en `mboxPC` en een omleidingsverzoek wordt teruggestuurd met een extra parameter (`mboxXDomainCheck=true`).

Als de browser cookies van derden accepteert, bevat de omleidingsaanvraag deze cookies en wordt de aanbieding geretourneerd.

Als de browser cookies van derden afwijst, worden deze cookies niet opgenomen in de omleidingsaanvraag en wordt standaardinhoud weergegeven voor alle locaties op de pagina. Omdat er geen cookies zijn ingesteld, vindt hetzelfde proces hierboven opnieuw plaats bij elke paginaaanvraag.

### Cookie-gedrag van derden en van derden

Het cookie van de andere fabrikant wordt opgeslagen in `clientcode.tt.omtrdc.net` en de cookie van de eerste partij wordt opgeslagen in `clientdomain.com`, waarbij `clientdomain` is uw domein.

at.js genereert een `mboxSession ID`. De eerste locatieaanvraag retourneert HTTP-antwoordheaders die proberen cookies van derden met een naam in te stellen `mboxSession` en `mboxPC`en er wordt een omleidingsverzoek teruggestuurd met een extra parameter (`mboxXDomainCheck=true`).

Als de browser cookies van derden accepteert, bevat de omleidingsaanvraag deze cookies en wordt de aanbieding geretourneerd.

Sommige browsers wijzen cookies van derden af. Als het cookie van een andere fabrikant wordt geblokkeerd, werkt het cookie van de eerste partij nog steeds. [!DNL Target] pogingen om het cookie van derden in te stellen, en als dit niet het geval is, dan [!DNL Target] kan alleen het specifieke domein van de client bijhouden. Interdomeintracering werkt niet als de derde wordt geblokkeerd, tenzij de `mboxSession` wordt toegevoegd in de verbinding die domeinen kruist. In dit geval wordt een ander cookie van de eerste fabrikant ingesteld en gesynchroniseerd met het cookie van het vorige domein.

## Cookie-instellingen

Het cookie heeft verschillende standaardinstellingen. U kunt deze instellingen desgewenst wijzigen, met uitzondering van de duur van het cookie. Vraag uw accountvertegenwoordiger wanneer u de cookie-instellingen wijzigt.

| Instelling | Informatie |
|--- |--- |
| Naam cookie | mbox. |
| Cookie-domein | Het tweede en bovenste niveau van de domeinen waaruit u de inhoud aanbiedt. Omdat het van het domein van uw bedrijf wordt gediend, is het koekje een eerste partijkoekje. Voorbeeld: `mycompany.com`. |
| Serverdomein | `clientcode.tt.omtrdc.net`, met de clientcode voor uw account. |
| Duur van cookie | Het cookie blijft twee jaar na de laatste aanmelding in de browser van de bezoeker staan.<P>De `deviceIdLifetime` instelling kan worden overschreven in [at.js versie 2.3.1 of hoger](../atjs/target-atjs-versions.md). Zie voor meer informatie [targetGlobalSettings()](../../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md). |
| P3P-beleid | De cookie wordt gepubliceerd met een P3P-beleid, zoals vereist door de standaardinstelling in de meeste browsers. Een P3P-beleid geeft aan welke browser de cookie aanbiedt en hoe de informatie wordt gebruikt. |

Het cookie houdt een aantal waarden bij voor het beheren van de manier waarop bezoekers campagnes ervaren:

| Waarde | Definitie |
|--- |--- |
| sessie-id | Een unieke id voor een gebruikerssessie. Standaard duurt dit 30 minuten. |
| pc-id | Een halfpermanente id voor de browser van een bezoeker. Laadt 14 dagen. |
| controleren | Een eenvoudige testwaarde die wordt gebruikt om te bepalen of een bezoeker cookies ondersteunt. Stel de instellingen in wanneer een bezoeker een pagina aanvraagt. |
| disable | Stel in of de laadtijd van de bezoeker langer is dan de time-out die is geconfigureerd in de Adobe Experience Platform Web SDK of het bestand at.js. Standaard duurt dit 1 uur. |

## Gevolgen voor [!DNL Target] voor Safari-bezoekers vanwege wijzigingen in het bijhouden van Apple WebKit

Houd rekening met het volgende:

### Hoe werkt [!DNL Adobe Target] Werk volgen?

| Cookies | Details |
|--- |--- |
| Domeinen van eerste partij | Dit is de standaardimplementatie voor [!DNL Target] klanten.  De &quot;mbox&quot;koekjes wordt geplaatst in het domein van de klant. |
| Tekstspatiëring van derden | Tekstspatiëring door derden is belangrijk voor reclame en doelgericht gebruik in gevallen waarin [!DNL Target] en in [!DNL Adobe Audience Manager] (AAM)  Bij het bijhouden van externe gegevens zijn technieken voor scripts die verwijzen naar andere sites, vereist.  [!DNL Target] gebruikt twee cookies, &quot;mboxSession&quot; en &quot;mboxPC&quot; ingesteld in het dialoogvenster `clientcode.tt.omtrd.net` domein. |

### Wat is de aanpak van Apple?

Uit Apple:

&quot;Intelligente preventie van tracering is een nieuwe WebKit-functie die het opsporen van gegevens via andere sites beperkt door cookies en andere websitegegevens verder te beperken.&quot;

&quot;Dit wordt intersite tracering genoemd en het cookie dat wordt gebruikt door `example-tracker.com` wordt een cookie van een andere fabrikant genoemd. In onze test vonden we populaire websites met meer dan 70 van dergelijke trackers, die allemaal ongemerkt gegevens over gebruikers verzamelen.&quot;

| Benadering | Details |
|--- |--- |
| Intelligente tracering | Zie voor meer informatie [Intelligente traceringspreventie](https://webkit.org/blog/7675/intelligent-tracking-prevention/) op de WebKit Open Source Web Browser Engine website. |
| Cookies | Hoe Safari cookies verwerkt:<ul><li>Cookies van derden die zich niet op een domein bevinden waartoe de gebruiker rechtstreeks toegang heeft, worden nooit opgeslagen. Dit gedrag is niet nieuw. Cookies van andere bedrijven worden al niet ondersteund in Safari.</li><li>Cookies van derden die zijn ingesteld op een domein waartoe de gebruiker rechtstreeks toegang heeft, worden na 24 uur gewist.</li><li>Cookies van de eerste partij worden na 30 dagen gezuiverd als dat domein van de eerste partij als het volgen van gebruikers over plaatsen is geclassificeerd. Deze kwestie zou op grote bedrijven kunnen van toepassing zijn die gebruikers naar verschillende domeinen online verzenden. Apple heeft niet duidelijk gemaakt hoe deze domeinen precies zullen worden geclassificeerd, of hoe een domein kan bepalen als zij als het volgen van gebruikers dwars-plaats zijn geclassificeerd.</li></ul> |
| Machine die leert domeinen te identificeren die naar andere sites verwijzen | Uit Apple:<P>Machine Learning Classifier: Een machine-leermodel wordt gebruikt om te classificeren welke hoogste privé-gecontroleerde domeinen de capaciteit hebben om de gebruiker dwars-plaats te volgen, die op de verzamelde statistieken wordt gebaseerd. Van de diverse verzamelde statistieken, bleken drie vectoren sterk signaal voor classificatie te hebben die op huidige volgende praktijken wordt gebaseerd: subresource onder aantal unieke domeinen, subframe onder aantal unieke domeinen, en aantal unieke domeinen opnieuw gericht aan. Alle gegevens verzamelen en classificeren gebeurt op het apparaat.<P>Nochtans, als de gebruiker met example.com als hoogste domein interactie heeft, die vaak als eerste - partijdomein wordt bedoeld, beschouwt de Intelligente het Volgen Preventie het signaal dat de gebruiker in de website geinteresseerd is en tijdelijk zijn gedrag zoals die in deze chronologie wordt getoond aanpast:<P>Als de gebruiker de laatste 24 uur contact heeft gehad met example.com, zijn cookies beschikbaar wanneer `example.com` is een derde. Dit staat voor &quot;Sign in met mijn rekening van X op Y&quot;login scenario&#39;s toe.<ul><li>Domeinen die als domein op het hoogste niveau worden bezocht, worden niet beïnvloed. Sites zoals bijvoorbeeld OKTA</li><li>Identificeert domeinen die subdomein of subframe zijn van de huidige pagina over meerdere unieke domeinen.</li></ul> |

### Hoe wordt Adobe beïnvloed?

| Betrokken functionaliteit | Details |
|--- |--- |
| Ondersteuning voor uitschakelen | Wijzigingen in WebKit voor Apple worden afgebroken.<P>[!DNL Target] de optie om te weigeren gebruikt een cookie in de `clientcode.tt.omtrdc.net` domein. Zie voor meer informatie [Privacy](/help/dev/before-implement/privacy/privacy.md).<P>[!DNL Target] ondersteunt twee opt-outs:<ul><li>Eén per client (de client beheert de koppeling om te weigeren).</li><li>Een via Adobe die de gebruiker uit alles opkiest [!DNL Target] functionaliteit voor alle klanten.</li></ul>Beide methoden gebruiken het cookie van derden. |
| [!DNL Target] activiteiten | Klanten kunnen hun [lengte van profielleven](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile-lifetime.html?lang=nl-NL) voor hun [!DNL Target] accounts—maximaal 90 dagen. Het probleem is dat als de profiellevensduur van de account langer is dan 30 dagen en de cookie van de eerste partij wordt gewist omdat het domein van de klant is gemarkeerd als het controleren van gebruikers naar andere sites, het gedrag voor Safari-bezoekers wordt beïnvloed in de volgende gebieden op [!DNL Target]:<P>**[!DNL Target]Rapporten**: Als een gebruiker Safari een activiteit ingaat, na 30 dagen terugkeert, en dan omzet, telt die gebruiker als twee bezoekers en één omzetting.<P>Dit gedrag is hetzelfde voor activiteiten die [!DNL Analytics] als bron van rapportage (A4T).<P>**Profiel en activiteitenlidmaatschap**:<ul><li>Profielgegevens worden gewist wanneer het cookie van de eerste partij verloopt.</li><li>Het lidmaatschap van de activiteit wordt gewist wanneer het eerste-partijkoekje verloopt.</li><li> [!DNL Target] werkt niet in Safari voor accounts die een cookie-implementatie van een andere fabrikant of een cookie-implementatie van een andere fabrikant gebruiken. Dit gedrag is niet nieuw. Safari heeft cookies van derden al een tijdje niet toegestaan.</li></ul><P>**Suggesties**: Als er een zorg is dat het klantendomein als één het volgen bezoekers dwars-zitting zou kunnen worden gemerkt, is het het veiligst om het profielleven aan 30 dagen of minder binnen te plaatsen [!DNL Target]. Dit zorgt ervoor dat gebruikers op dezelfde manier worden bijgehouden in Safari en alle andere browsers. |
