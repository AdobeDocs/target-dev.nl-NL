---
keywords: systeemdiagram, flikkering, at.js, implementatie, javascript bibliotheek, js, atjs, $8
description: Meer informatie over [!DNL Target] in.js JavaScript-bibliotheekfuncties, waaronder systeemdiagrammen, waarmee u de workflow tijdens het laden van pagina's kunt begrijpen.
title: Hoe werkt de JavaScript-bibliotheek at.js?
feature: at.js
exl-id: 9183797c-857b-4b7f-a573-6bb1d583f7b1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 2%

---

# Hoe werkt at.js

Om [!DNL Adobe Target] aan clientzijde, moet u de JavaScript-bibliotheek at.js gebruiken.

Bij een clientimplementatie van [!DNL Adobe Target], [!DNL Target] levert de ervaringen verbonden aan een activiteit rechtstreeks aan cliëntbrowser. De browser bepaalt welke ervaring wordt weergegeven en geeft deze weer. Met een cliënt-zijimplementatie, kunt u een redacteur gebruiken WYSIWYG, [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) of een niet-visuele interface [Form-based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), om uw test- en personaliservaringen te maken.

## Wat is at.js?

De bibliotheek at.js is de implementatiebibliotheek voor client-side implementatie van [!DNL Adobe Target]. De bibliotheek at.js verbetert de laadtijden voor webimplementaties en biedt betere implementatieopties voor toepassingen van één pagina. at.js is de aanbevolen implementatiebibliotheek en wordt regelmatig bijgewerkt met nieuwe mogelijkheden. Wij adviseren dat alle klanten uitvoeren of aan migreren [nieuwste versie van at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md).

Zie voor meer informatie [JavaScript-doelbibliotheken](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#libraries).

In de [!DNL Target]de volgende Adobe Experience Cloud-oplossingen worden geïmplementeerd: [!DNL Analytics], Doel en [!DNL Audience Manager]. Daarnaast worden de volgende [!DNL Experience Cloud] de kerndiensten worden uitgevoerd : [!DNL Adobe Experience Platform], [!UICONTROL Audiences], en [!UICONTROL Visitor ID Service].

## Wat is het verschil tussen at.js 1.*x* en werkstroomdiagrammen bij .js 2.x?

Zie [Bijwerken van at.js 1.x naar at.js 2.x](/help/dev/implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md) voor meer informatie over de verschillen die in 2.O van 1 werden ingevoerd.*x*.

Vanuit een weergave op hoog niveau zijn er enkele verschillen tussen de twee versies:

* at.js 2.x heeft geen globaal mbox verzoekconcept maar eerder een pagina-lading verzoek. Een verzoek om pagina&#39;s te laden kan worden beschouwd als een verzoek om inhoud op te halen die moet worden toegepast op het eerste laadmoment van de pagina van uw website.
* at.js 2.x beheert de concepten die [!UICONTROL Views], die worden gebruikt voor toepassingen voor één pagina (SPA). te.js 1.*x* is zich niet bewust van dit concept.

## at.js 2.x-diagrammen

De volgende diagrammen helpen u het werkschema van at.js 2.x begrijpen met [!UICONTROL Views] en hoe dit de integratie van de SPA verbetert . Voor een betere inleiding van de concepten die in at.js 2.x worden gebruikt, zie [Toepassing van één pagina](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![Doelstroom met at.js 2.x](/help/dev/implement/client-side/assets/system-diagram-atjs-20.png "Doelstroom met at.js 2.x"){zoomable="yes"}

| Stap | Details |
| --- | --- |
| 1 | De vraag keert terug [!UICONTROL Experience Cloud ID] als de gebruiker voor authentiek wordt verklaard; een andere vraag synchroniseert de klantenidentiteitskaart |
| 2 | De bibliotheek at.js wordt synchroon geladen en de hoofdtekst van het document verborgen.<br />at.js kan ook asynchroon worden geladen met een optioneel vooraf verborgen fragment dat op de pagina is geïmplementeerd. |
| 3 | Er wordt een aanvraag voor het laden van een pagina ingediend, inclusief alle geconfigureerde parameters (MCID, SDID en klant-id). |
| 4 | Profielscripts worden uitgevoerd en vervolgens toegevoegd aan het dialoogvenster [!UICONTROL Profile Store]. De Stoverzoeken om gekwalificeerd publiek van de [!UICONTROL Audience Library] (bijvoorbeeld publiek dat wordt gedeeld vanuit [!DNL Adobe Analytics], [!DNL Audience Manager], enz.).<br />Klantkenmerken worden naar de [!UICONTROL Profile Store] in een batchproces. |
| 5 | Gebaseerd op parameters en profielgegevens van het URL-verzoek, [!DNL Target] bepaalt welke activiteiten en ervaringen u wilt retourneren aan de bezoeker voor de huidige pagina en de toekomstige weergaven. |
| 6 | Gerichte inhoud wordt teruggestuurd naar de pagina, waarbij eventueel ook profielwaarden voor extra personalisatie worden opgenomen.<br />Gerichte inhoud op de huidige pagina wordt zo snel mogelijk zichtbaar zonder flikkering van de standaardinhoud.<br />Gerichte inhoud voor weergaven die worden weergegeven als gevolg van gebruikershandelingen in een SPA, wordt in de browser in cache geplaatst, zodat deze direct kan worden toegepast zonder een extra serveraanroep wanneer de weergaven worden geactiveerd `triggerView()`. |
| 7 | Analysegegevens worden verzonden naar [!UICONTROL Data Collection] servers. |
| 8 | De gerichte gegevens worden aangepast aan de analysegegevens via SDID en worden verwerkt in de [!DNL Analytics] rapporteringsopslag.<br />[!DNL Analytics] gegevens kunnen vervolgens in beide worden weergegeven [!DNL Analytics] en [!DNL Target] via (A4T) rapporten. |

Nu, overal `triggerView()` wordt geïmplementeerd op uw SPA, [!UICONTROL Views] en de acties worden teruggewonnen uit geheim voorgeheugen en aan de gebruiker getoond zonder een servervraag. `triggerView()` verzoekt de Commissie tevens [!DNL Target] achterkant om het aantal beeldingen te verhogen en op te nemen. Ga voor meer informatie over at.js voor SPA met Weergaven naar [Toepassing van één pagina](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![Doelstroom bij.js 2.x triggerView](/help/dev/implement/client-side/assets/atjs-20-triggerview.png "Doelstroom bij.js 2.x triggerView"){zoomable="yes"}

| Stap | Details |
| --- | --- |
| 1 | `triggerView()` wordt in de SPA aangeroepen om de [!UICONTROL View] en past handelingen toe om visuele elementen te wijzigen. |
| 2 | De gerichte inhoud voor de mening wordt gelezen van het geheime voorgeheugen. |
| 3 | Gerichte inhoud wordt zo snel mogelijk zichtbaar zonder flikkering van de standaardinhoud. |
| 4 | Aanmelding wordt verzonden naar de [!DNL Target] [!UICONTROL Profile Store] om de bezoeker te tellen in de activiteit en verhogingsmetriek. |
| 5 | [!DNL Analytics] gegevens verzonden naar [!UICONTROL Data Collection Servers]. |
| 6 | [!DNL Target] gegevens komen overeen met [!DNL Analytics] gegevens via de SDID en worden verwerkt in de [!DNL Analytics] rapporteringsopslag. [!DNL Analytics] gegevens kunnen vervolgens in beide worden weergegeven [!DNL Analytics] en [!DNL Target] via A4T-rapporten. |

### Video - op.js 2.x architecturaal diagram

at.js 2.x verbetert de Adobe Target-ondersteuning voor SPA en integreert deze met andere Experience Cloud-oplossingen. In deze video wordt uitgelegd hoe alles bij elkaar komt.

>[!VIDEO](https://video.tv.adobe.com/v/26250/?quality=12)

Zie [Begrijpen hoe at.js 2.x werkt](https://experienceleague.adobe.com/docs/target-learn/tutorials/implementation/understanding-how-atjs-20-works.html) voor meer informatie .

## bij.js 1.x-diagram

Met de volgende diagrammen krijgt u inzicht in de workflow van at.js 1.x.

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![Doelstroom bij.js 1.x](/help/dev/implement/client-side/assets/target-flow.png "Doelstroom bij.js 1.x"){zoomable="yes"}

| Stap | Beschrijving | Bellen | Beschrijving |
|--- |--- |--- |--- |
| 1 | De vraag keert identiteitskaart van de Experience Cloud terug (MCID) als de gebruiker voor authentiek wordt verklaard; een andere vraag synchroniseert de klantenidentiteitskaart | 2 | De bibliotheek at.js wordt synchroon geladen en de hoofdtekst van het document verborgen. |
| 3 | Er wordt een globaal mbox-verzoek ingediend, inclusief alle geconfigureerde parameters, MCID, SDID en klant-id (optioneel). | 4 | Profielscripts worden uitgevoerd en vervolgens toegevoegd aan de profielenwinkel. De winkel vraagt om gekwalificeerd publiek uit de Audience Library (bijvoorbeeld publiek dat wordt gedeeld vanuit Adobe Analytics, Audience Manager, enz.).<br />Klantkenmerken worden in een batchproces naar de profielopslag verzonden. |
| 5 | Gebaseerd op URL, mbox parameters, en profielgegevens, [!DNL Target] bepaalt welke activiteiten en ervaringen moeten worden teruggegeven aan de bezoeker. | 6 | Gerichte inhoud wordt teruggestuurd naar pagina, met eventueel ook profielwaarden voor extra personalisatie.<br />De ervaring wordt zo snel mogelijk getoond zonder flikkering van standaardinhoud. |
| 7 | De analysegegevens worden verzonden naar de servers van de Inzameling van Gegevens. | 8 | De doelgegevens worden via de SDID aangepast aan de analysegegevens en worden verwerkt in de analytische rapportageopslag.<br />De analysegegevens kunnen dan zowel in Analytics als  [!DNL Target] via [!UICONTROL Analytics for Target] (A4T) verslagen. |

### Video - kantooruren: tips en een overzicht op at.js (26 juni 2019)

Deze video is een opname van &quot;Office Hours&quot;, een initiatief onder leiding van de [!UICONTROL Adobe Customer Care] team.

* Voordelen van het gebruik van at.js
* at.js-instellingen
* Flikkerverwerking
* Foutopsporing bij.js
* Bekende problemen
* Veelgestelde vragen

>[!VIDEO](https://video.tv.adobe.com/v/27959/?quality=12)

## Hoe at.js aanbiedingen met HTML-inhoud rendert

Bij rendering van aanbiedingen met HTML-inhoud past at.js het volgende algoritme toe:

1. Afbeeldingen worden vooraf geladen (als er `<img>` -tags in HTML-inhoud).

1. HTML-inhoud is gekoppeld aan het DOM-knooppunt.

1. Inline scripts worden uitgevoerd (code omsloten in `<script>` -tags).

1. Externe scripts worden asynchroon geladen en uitgevoerd (`<script>` tags met `src` kenmerken).

Belangrijke opmerkingen:

* at.js verstrekt geen garanties op de orde van verre manuscriptuitvoering, aangezien deze asynchroon worden geladen.
* Inline scripts mogen geen afhankelijkheden hebben van externe scripts, omdat deze later worden geladen en uitgevoerd.
