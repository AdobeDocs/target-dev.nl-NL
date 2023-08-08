---
title: Recommendations ophalen met de leverings-API
description: Dit artikel begeleidt ontwikkelaars door de stappen die nodig zijn om aanbevelingen op te halen met de Adobe Target Delivery API.
feature: APIs/SDKs, Recommendations, Administration & Configuration
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 9b391f42-2922-48e0-ad7e-10edd6125be6
source-git-commit: ba53161b2ec51af3d90994773034790feb51099c
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 0%

---

# Recommendations ophalen met de leverings-API

De Adobe Target- en Adobe Target Recommendations-API&#39;s kunnen worden gebruikt om reacties op webpagina&#39;s te leveren, maar kunnen ook worden gebruikt in ervaringen die niet op HTML zijn gebaseerd, zoals apps, schermen, consoles, e-mails, kiosken en andere weergaveapparaten. Met andere woorden, wanneer doelbibliotheken en JavaScript niet kunnen worden gebruikt, wordt de [API voor doellevering](/help/dev/implement/delivery-api/overview.md) laat nog toegang tot het volledige gamma van de functionaliteit van het Doel toe, om gepersonaliseerde ervaringen te leveren.

>[!NOTE]
>
>Gebruik de API voor doellevering wanneer u inhoud aanvraagt met feitelijke aanbevelingen (aanbevolen producten of onderdelen).

Om aanbevelingen terug te winnen, verzend een vraag van de POST van de Levering API van Adobe Target met de aangewezen contextuele informatie, die een gebruiker - identiteitskaart (voor gebruik met profiel-specifieke aanbevelingen zoals onlangs bekeken punten van de gebruiker), relevante mbox naam, mbox parameters, profielparameters, of andere attributen kan omvatten. De reactie zal geadviseerde entiteit.ids (en kan andere entiteitgegevens omvatten) in formaat JSON of HTML omvatten, die dan in het apparaat kunnen worden getoond.

De [Leverings-API](/help/dev/implement/delivery-api/overview.md) voor Adobe Target beschikbaar maakt alle bestaande functies die een standaardaanvraag van Target biedt.

De leverings-API:

* Laat u toe om ervaringen of aanbiedingen voor een plaats en een publiek op een RESTful manier terug te winnen.
* Geen verificatie vereist.
* Alleen POST&#39;s.
* Verwerkt geen cookies of richt geen aanroepen om.
* Vereist of herkent geen &quot;gebruikersrollen.&quot; Het haalt eenvoudig inhoud op of rapporteert gebeurtenissen aan de Edge-servers van het Doel.

De leverings-API gebruiken om de ervaringen van het Doel-met inbegrip van aanbevelingen-te leveren:

1. Creeer een activiteit van het Doel (A/B, XT, AP, of Recommendations) gebruikend Form-Based Composer (niet de Visuele Composer van de Ervaring).
1. Gebruik de leverings-API om een reactie op te halen voor de aanvragen die worden gegenereerd door de doelactiviteit die u zojuist hebt gemaakt.

&lt;!— Q: Waarom zijn BEIDE stappen hiervoor nodig? Als u een op vorm-Gebaseerde aanbeveling hebt die voor een mbox wordt bepaald, wat is het punt/voordeel van OOK het hebben van de stap van levering API binnen om resultaten terug te winnen? Waarom kunt u niet enkel op vorm-gebaseerde Rec de resultaten in het bestemmingsapparaat...? hebben? A: Zie onderstaande kwestie gebruiken... Het is wanneer u de hangende resultaten wilt &quot;onderscheppen&quot;om meer te doen alvorens de resultaten te tonen. Dingen zoals vergelijkingen in real time met inventarisniveaus. --->

## Een aanbeveling maken met de Form-based Experience Composer

Als u aanbevelingen wilt maken die u met de API voor aflevering kunt gebruiken, gebruikt u de opdracht [Op formulieren gebaseerde composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html).

1. Maak eerst een JSON-ontwerp en sla dit op dat u in uw aanbeveling wilt gebruiken. Voor voorbeeld JSON, plus achtergrondinformatie over hoe de reacties JSON kunnen worden teruggekeerd wanneer het vormen van een op vorm-gebaseerde activiteit, zie de documentatie over [Aanbevelingsontwerpen maken](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html). In dit voorbeeld krijgt het ontwerp de naam *Eenvoudige JSON.*
   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

1. Ga in Doel naar **[!UICONTROL Activities]** > **[!UICONTROL Create Activity]** > **[!UICONTROL Recommendations]** selecteert u vervolgens **[!UICONTROL Form]**.

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

1. Selecteer een eigenschap en klik op **[!UICONTROL Next]**.
1. Bepaal de plaats waar u gebruikers de reactie van de aanbeveling wilt ontvangen. In het onderstaande voorbeeld wordt een locatie gebruikt met de naam *api_charter*. Selecteer uw JSON-ontwerp, dat u eerder hebt gemaakt, met de naam *Eenvoudige JSON.*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
1. Sla de aanbeveling op en activeer deze. Het zal resultaten opleveren. [Zodra de resultaten klaar zijn](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html), kunt u de leverings-API gebruiken om deze op te halen.

## De API voor aflevering gebruiken

De syntaxis voor de [Leverings-API](/help/dev/implement/delivery-api/overview.md) is:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. Let op: de clientcode is vereist. Ter herinnering: je clientcode kan in Adobe Target worden gevonden door naar **[!UICONTROL Recommendations]** > **[!UICONTROL Settings]**. Noteer de **Clientcode** waarde in de **API-token voor aanbeveling** sectie.
   ![client-code.png](assets/client-code.png)
1. Zodra u uw cliëntcode hebt, construeer uw levering API vraag. Het onderstaande voorbeeld begint met het **[!UICONTROL Web Batched Mboxes Delivery API Call]** in de [Delivery API Postman-collectie](../../implement/delivery-api/overview.md/#section/Getting-Started/Postman-Collection), waarbij relevante wijzigingen worden aangebracht. Bijvoorbeeld:
   * de **browser** en **adres** objecten zijn verwijderd uit de **Lichaam**, aangezien deze niet vereist zijn voor gevallen van niet-HTML gebruik
   * *api_charter* wordt vermeld als locatienaam in dit voorbeeld
   * de entiteit.id wordt opgegeven, omdat deze aanbeveling is gebaseerd op Content Gelijksheid, waarvoor een huidige itemsleutel moet worden doorgegeven aan Target.
     ![server-side-Delivery-API-call.png](assets/server-side-delivery-api-call2.png)
Herinner me om uw vraagparameters correct te vormen. Zorg er bijvoorbeeld voor dat u `{{CLIENT_CODE}}` indien nodig. &lt;!— Q: In de bijgewerkte vraagsyntaxis, wordt entity.id vermeld als profileParameter in plaats van een mboxParameter zoals in oudere versies. ---> &lt;!— Q: Oude afbeelding ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Oude begeleidende tekst: &quot;Deze aanbeveling is gebaseerd op inhoud Vergelijkbare producten op basis van de entiteit.id die via mboxParameters is verzonden.&quot; —>
     ![client-code3](assets/client-code3.png)
1. Verzend de aanvraag. Dit wordt uitgevoerd tegen de *api_charter* -locatie, waarop een actieve aanbeveling wordt uitgevoerd, gedefinieerd met uw JSON-ontwerp dat een lijst met aanbevolen entiteiten uitvoert.
1. Ontvang een reactie op basis van het JSON-ontwerp.
   ![server-side-create-recs-json-response2.png](assets/server-side-create-recs-json-response2.png)
De reactie omvat de sleutel-id en de entiteit-id&#39;s van de aanbevolen entiteiten.

Als u de API voor levering op deze manier gebruikt met Recommendations, kunt u aanvullende stappen uitvoeren voordat u aanbevelingen weergeeft aan de bezoeker op het niet-HTML-apparaat. U kunt bijvoorbeeld de reactie van de API voor aflevering gebruiken om een extra, realtime zoekopdracht uit te voeren naar de details van de entiteitskenmerken (inventaris, prijs, classificatie, enzovoort) van een ander systeem (zoals een CMS-, PIM- of e-commerce-platform) voordat u de uiteindelijke resultaten weergeeft.

Met behulp van de aanpak die in deze handleiding wordt beschreven, kunt u elke toepassing gebruiken om de reactie van Target te benutten en persoonlijke aanbevelingen te doen!

## Voorbeeldimplementaties

De volgende bronnen bieden voorbeelden van verschillende implementaties die niet gericht zijn op HTML. Houd er rekening mee dat elke implementatie uniek zal zijn, vanwege het systeem en de apparaten in kwestie.

| Bron | Details |
| --- | --- |
| [Adobe Target Overal - Implementeer server-kant of in de IoT](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Summit 2019 Lab die praktijkervaring biedt voor een React-toepassing die gebruikmaakt van Adobe Target server-side API&#39;s. |
| [Adobe Target in een mobiele toepassing zonder de Adobe-SDK](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | In deze handleiding ziet u hoe u Adobe Target kunt instellen in uw mobiele app zonder de SDK van de Adobe te installeren. Deze oplossing gebruikt de webweergave van Tealium SDK en de module Externe opdrachten om aanvragen te verzenden en te ontvangen naar de Adobe Visitor API (Experience Cloud) en de Adobe Target API. |
| [De doelextensie configureren in Experience Platform Launch en doel-API&#39;s implementeren](https://developer.adobe.com/client-sdks/documentation/adobe-target/) | Stappen voor het vormen van de uitbreiding van het Doel in Experience Platform Launch, het toevoegen van de Uitbreiding van het Doel aan uw app, en het uitvoeren van Doel APIs aan verzoekactiviteiten, prefetch aanbiedingen, en Ga visuele voorproefwijze in. |
| [Adobe Target Node-client](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | Open-sourced Target Node.js SDK v1.0 |
| [Overzicht van de server](../../implement/server-side/server-side-overview.md) | Informatie over Adobe Target Server Side Delivery API&#39;s, Server Side Batch Delivery API&#39;s, Node.js SDK en Adobe Target Recommendations API&#39;s. |
| [Adobe Campaign Content Recommendations in Email](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Blog waarin wordt beschreven hoe u via Adobe Target en Adobe I/O Runtime in Adobe Campaign aanbevelingen kunt doen voor inhoud in e-mail. |

## Recommendations Setup beheren met API&#39;s

Meestal worden aanbevelingen geconfigureerd in de gebruikersinterface van Adobe Target en vervolgens gebruikt of benaderd via de doel-API&#39;s, om redenen zoals die vermeld zijn in de bovenstaande secties. Deze UI-API-coördinatie komt veel voor. Soms willen gebruikers echter wel alle handelingen uitvoeren via API&#39;s, zowel de setup als het gebruik van resultaten. Hoewel veel minder vaak, kunnen de gebruikers absoluut vormen, uitvoeren, *en* de resultaten van aanbevelingen volledig te benutten met behulp van de API&#39;s.

We leerden in een [eerdere secties](manage-catalog.md) hoe u Adobe Target Recommendations-entiteiten beheert en op de server aanbiedt. Op dezelfde manier [Adobe Developer Console](https://developer.adobe.com/console/home) kunt u criteria, promoties, verzamelingen en ontwerpsjablonen beheren zonder u aan te melden bij Adobe Target. Een volledige lijst van alle Recommendations API&#39;s is te vinden [hier](http://developers.adobetarget.com/api/recommendations/), maar hier is een samenvatting ter referentie.

| Bron | Details |
| --- | --- |
| [Verzamelingen](http://developers.adobetarget.com/api/recommendations/#tag/Collections) | Verzamelingen weergeven, maken, ophalen, bewerken en verwijderen. |
| [Criteria](http://developers.adobetarget.com/api/recommendations/#tag/Criteria) | Lijst en krijg criteria. |
| [Ontwerpen](http://developers.adobetarget.com/api/recommendations/#tag/Designs) | Ontwerp weergeven, maken, ophalen, bewerken, verwijderen en valideren. |
| [Entiteiten](http://developers.adobetarget.com/api/recommendations/#tag/Entities) | Entiteiten opslaan, verwijderen en ophalen. |
| [Aanbiedingen](http://developers.adobetarget.com/api/recommendations/#tag/Promotions) | Promoties aanbieden, maken, ophalen, bewerken en verwijderen. |
| [Categoriecriteria](http://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | Categoriecriteria weergeven, maken, ophalen, bewerken en verwijderen. |
| [Aangepaste criteria](http://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | Aangepaste criteria weergeven, maken, ophalen, bewerken en verwijderen. |
| [Objectcriteria](http://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | Objectcriteria weergeven, maken, ophalen, bewerken en verwijderen. |
| [Criteria voor populariteit](http://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | Maak een lijst, maak, krijg, bewerk en verwijder populiteitscriteria. |
| [Kenmerkcriteria profiel](http://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | Criteria voor profielkenmerken weergeven, maken, ophalen, bewerken en verwijderen. |
| [Recente criteria](http://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | Recente criteria weergeven, maken, ophalen, bewerken en verwijderen. |
| [Reekscriteria](http://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | U kunt volgreekscriteria weergeven, maken, ophalen, bewerken en verwijderen. |

## Referentiedocumentatie

* [Adobe Target Delivery API-documentatie](/help/dev/implement/delivery-api/overview.md)
* [Recommendations integreren met e-mail](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## Samenvatting en revisie

Gefeliciteerd! Door deze gids in te vullen, hebt u geleerd hoe te:
* [Uw catalogus beheren met de Recommendations API](manage-catalog.md)
* [Aangepaste criteria beheren met de Recommendations API](manage-custom-criteria.md)
* [De leverings-API gebruiken met Recommendations](fetch-recs-server-side-delivery-api.md)
