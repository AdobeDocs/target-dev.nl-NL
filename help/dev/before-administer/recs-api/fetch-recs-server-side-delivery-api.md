---
title: Aanbevelingen ophalen met de leverings-API
description: Dit artikel begeleidt ontwikkelaars door de stappen die nodig zijn om aanbevelingen op te halen met de Adobe Target Delivery API.
feature: APIs/SDKs, Recommendations, Administration & Configuration
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 9b391f42-2922-48e0-ad7e-10edd6125be6
source-git-commit: 526445fccee9b778b7ac0d7245338f235f11d333
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 0%

---

# Aanbevelingen ophalen met de leverings-API

De API&#39;s voor Adobe Target- en Adobe Target-aanbevelingen kunnen worden gebruikt om reacties op webpagina&#39;s te leveren, maar kunnen ook worden gebruikt in ervaringen die niet op HTML zijn gebaseerd, zoals apps, schermen, consoles, e-mails, kiosken en andere weergaveapparaten. Met andere woorden, wanneer de bibliotheken van het Doel en JavaScript niet kunnen worden gebruikt, laat [&#x200B; Levering API van het Doel &#x200B;](/help/dev/implement/delivery-api/overview.md) nog toegang tot de volledige waaier van de functionaliteit van het Doel toe, om gepersonaliseerde ervaringen te leveren.

>[!NOTE]
>
>Gebruik de API voor doellevering wanneer u inhoud aanvraagt met feitelijke aanbevelingen (aanbevolen producten of onderdelen).

Als u aanbevelingen wilt opvragen, stuurt u een POST-aanroep van de Adobe Target Delivery API met de relevante contextafhankelijke informatie. Deze kan een gebruikers-id bevatten (voor gebruik met profielspecifieke aanbevelingen zoals de onlangs bekeken items van de gebruiker), relevante mbox-naam, mbox-parameters, profielparameters of andere kenmerken. De reactie zal geadviseerde entiteit.ids (en kan andere entiteitgegevens omvatten) in formaat JSON of HTML omvatten, die dan in het apparaat kan worden getoond.

De [&#x200B; Levering API &#x200B;](/help/dev/implement/delivery-api/overview.md) voor Adobe Target stelt alle bestaande eigenschappen bloot die een standaardverzoek van het Doel verstrekt.

De leverings-API:

* Laat u toe om ervaringen of aanbiedingen voor een plaats en een publiek op een RESTful manier terug te winnen.
* Geen verificatie vereist.
* Alleen POST&#39;s.
* Verwerkt geen cookies of richt geen aanroepen om.
* Vereist of herkent geen &quot;gebruikersrollen.&quot; Het haalt eenvoudig inhoud op of rapporteert gebeurtenissen aan de Edge-servers van het Doel.

De leverings-API gebruiken om de ervaringen van het Doel-met inbegrip van aanbevelingen-te leveren:

1. Creeer een activiteit van het Doel (A/B, XT, AP, of Aanbevelingen) gebruikend Form-Based Composer (niet de Visuele Composer van de Ervaring).
1. Gebruik de leverings-API om een reactie op te halen voor de aanvragen die worden gegenereerd door de doelactiviteit die u zojuist hebt gemaakt.

&lt;!— Q: Waarom zijn BEIDE stappen hiervoor nodig? Als u een op vorm-Gebaseerde aanbeveling hebt die voor een mbox wordt bepaald, wat is het punt/voordeel van OOK het hebben van de stap van levering API binnen om resultaten terug te winnen? Waarom kunt u niet enkel op vorm-gebaseerde Rec de resultaten in het bestemmingsapparaat...? hebben? A: Zie onderstaande kwestie gebruiken... Het is wanneer u de hangende resultaten wilt &quot;onderscheppen&quot;om meer te doen alvorens de resultaten te tonen. Dingen zoals vergelijkingen in real time met inventarisniveaus. —>

## Een aanbeveling maken met de Form-based Experience Composer

Om aanbevelingen tot stand te brengen die met levering API kunnen worden gebruikt, gebruik [&#x200B; op vorm-gebaseerde Composer &#x200B;](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=nl-NL).

1. Maak eerst een JSON-ontwerp en sla dit op dat u in uw aanbeveling wilt gebruiken. Voor steekproef JSON, plus achtergrondinformatie betreffende hoe de reacties JSON kunnen zijn teruggekeerd wanneer het vormen van een op vorm-gebaseerde activiteit, zie de documentatie bij [&#x200B; Creërend de Ontwerpen van de Aanbeveling &#x200B;](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html?lang=nl-NL). In dit voorbeeld, wordt het ontwerp genoemd *Eenvoudige JSON.*
   ![&#x200B; server-kant-creeer-recs-json-design.png &#x200B;](assets/server-side-create-recs-json-design.png)

1. Navigeer in Doel naar **[!UICONTROL Activities]** > **[!UICONTROL Create Activity]** > **[!UICONTROL Recommendations]** en selecteer vervolgens **[!UICONTROL Form]** .

   ![&#x200B; server-kant-creeer-recs.png &#x200B;](assets/server-side-create-recs.png)

1. Selecteer een eigenschap en klik op **[!UICONTROL Next]** .
1. Bepaal de plaats waar u gebruikers de reactie van de aanbeveling wilt ontvangen. Het voorbeeld gebruikt hieronder een plaats genoemd *api_charter*. Selecteer uw op JSON-Gebaseerd ontwerp, vroeger gecreeerd, genoemd *Eenvoudige JSON.*
   ![&#x200B; server-kant-creeer-recs-form.png &#x200B;](assets/server-side-create-recs-form1.png)
1. Sla de aanbeveling op en activeer deze. Het zal resultaten opleveren. [&#x200B; Zodra de resultaten klaar &#x200B;](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html?lang=nl-NL) zijn, kunt u levering API gebruiken om hen terug te winnen.

## De API voor aflevering gebruiken

De syntaxis voor [&#x200B; Levering API &#x200B;](/help/dev/implement/delivery-api/overview.md) is:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. Let op: de clientcode is vereist. Ter herinnering, uw clientcode kunt u vinden in Adobe Target door naar **[!UICONTROL Recommendations]** > **[!UICONTROL Settings]** te navigeren. Noteer de **waarde van de Code van de 0&rbrace; Cliënt in de** Symbolische van Aanbeveling API **sectie.**
   ![&#x200B; cliënt-code.png &#x200B;](assets/client-code.png)
1. Zodra u uw cliëntcode hebt, construeer uw levering API vraag. Het voorbeeld hieronder begint met **[!UICONTROL Web Batched Mboxes Delivery API Call]** die in de [&#x200B; levering API inzameling van Postman &#x200B;](../../implement/delivery-api/overview.md/#section/Getting-Started/Postman-Collection) wordt verstrekt, die relevante wijzigingen aanbrengen. Bijvoorbeeld:
   * de **browser** en **adres** voorwerpen werden verwijderd uit het **Lichaam**, aangezien zij niet voor niet-HTML gebruiksgevallen worden vereist
   * *api_charter* is vermeld als plaatsnaam in dit voorbeeld
   * de entiteit.id wordt opgegeven, omdat deze aanbeveling is gebaseerd op Content Gelijksheid, waarvoor een huidige itemsleutel moet worden doorgegeven aan Target.

     ![&#x200B; server-zij-levering-API-call.png &#x200B;](assets/server-side-delivery-api-call2.png)
Herinner me om uw vraagparameters correct te vormen. Stel bijvoorbeeld dat u `{{CLIENT_CODE}}` opgeeft als dat nodig is. &lt;!— Q: In de bijgewerkte vraagsyntaxis, wordt entity.id vermeld als profileParameter in plaats van een mboxParameter zoals in oudere versies. —> &lt;!— Q: Oude beeld ![&#x200B; server-kant-creatie-recs-post.png &#x200B;](assets/server-side-create-recs-post.png) Oude begeleidende tekst: &quot;Merk op deze aanbeveling gebaseerd op Inhoud Vergelijkbare producten die op entiteit.id worden gebaseerd die via mboxParameters wordt verzonden.&quot; —>
     ![&#x200B; cliënt-code3 &#x200B;](assets/client-code3.png)
1. Verzend de aanvraag. Dit voert tegen *api_charter* plaats uit, die een actieve aanbeveling heeft die op het loopt, die met uw ontwerp JSON wordt bepaald dat een lijst van geadviseerde entiteiten zal uitvoeren.
1. Ontvang een reactie op basis van het JSON-ontwerp.
   ![&#x200B; server-kant-creeer-recs-json-response2.png &#x200B;](assets/server-side-create-recs-json-response2.png)
De reactie omvat de sleutel-id en de entiteit-id&#39;s van de aanbevolen entiteiten.

Als u de API voor levering op deze manier gebruikt met aanbevelingen, kunt u aanvullende stappen uitvoeren voordat u aanbevelingen weergeeft aan de bezoeker op het niet-HTML-apparaat. U kunt bijvoorbeeld de reactie van de API voor aflevering gebruiken om een extra, realtime zoekopdracht uit te voeren naar de details van de entiteitskenmerken (inventarisatie, prijs, classificatie, enzovoort) van een ander systeem (zoals een CMS-, PIM- of e-commerce-platform) voordat u de uiteindelijke resultaten weergeeft.

Met behulp van de aanpak die in deze handleiding wordt beschreven, kunt u elke toepassing gebruiken om de reactie van Target te benutten en persoonlijke aanbevelingen te doen!

## Voorbeeldimplementaties

De volgende bronnen bieden voorbeelden van verschillende implementaties die niet gericht zijn op HTML. Houd er rekening mee dat elke implementatie uniek zal zijn, vanwege het systeem en de apparaten in kwestie.

| Bron | Details |
| --- | --- |
| [&#x200B; Vormend de uitbreiding van het Doel in de Lancering van het Platform van de Ervaring en het Uitvoeren van Doel APIs &#x200B;](https://developer.adobe.com/client-sdks/documentation/adobe-target/) | Stappen voor het vormen van de uitbreiding van het Doel in de Lancering van het Platform van de Ervaring, het toevoegen van de Uitbreiding van het Doel aan uw app, en het uitvoeren van Doel APIs aan verzoekactiviteiten, prefetch aanbiedingen, en Ga visuele voorproefwijze in. |
| [&#x200B; Cliënt van de Knoop van Adobe Target &#x200B;](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | Open-sourced Target Node.js SDK v1.0 |
| [&#x200B; Zijoverzicht van de Server &#x200B;](../../implement/server-side/server-side-overview.md) | Informatie over Adobe Target Server Side Delivery API&#39;s, Server Side Batch Delivery API&#39;s, Node.js SDK en Adobe Target Recommendations API&#39;s. |
| [&#x200B; de Aanbevelingen van de Inhoud van Adobe Campaign in E-mail &#x200B;](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Blog waarin wordt beschreven hoe u via Adobe Target en Adobe I/O Runtime in Adobe Campaign aanbevelingen kunt doen voor inhoud in e-mail. |

## Installatie van aanbevelingen beheren met API&#39;s

Meestal worden aanbevelingen geconfigureerd in de gebruikersinterface van Adobe Target en vervolgens gebruikt of benaderd via de doel-API&#39;s, om redenen zoals die vermeld zijn in de bovenstaande secties. Deze UI-API-coördinatie komt veel voor. Soms willen gebruikers echter wel alle handelingen uitvoeren via API&#39;s, zowel de setup als het gebruik van resultaten. Hoewel veel minder gemeenschappelijk, kunnen de gebruikers absoluut vormen, uitvoeren, *en* hefboomwerking de resultaten van aanbevelingen volledig gebruikend APIs.

Wij leerden in een [&#x200B; vroegere sectie &#x200B;](manage-catalog.md) hoe te om de entiteiten van de Aanbevelingen van Adobe Target te beheren en hen server-kant te leveren. Op dezelfde manier [&#x200B; Adobe Developer Console &#x200B;](https://developer.adobe.com/console/home) staat u toe om criteria, bevorderingen, inzamelingen, en ontwerpmalplaatjes te beheren zonder het moeten login aan Adobe Target. Een volledige lijst van alle Aanbevelingen APIs kan [&#x200B; hier &#x200B;](https://developer.adobe.com/target/administer/recommendations-api/) worden gevonden, maar hier is een samenvatting voor verwijzing.

| Bron | Details |
| --- | --- |
| [&#x200B; Inzamelingen &#x200B;](https://developer.adobe.com/target/administer/recommendations-api/#tag/Collections) | Verzamelingen weergeven, maken, ophalen, bewerken en verwijderen. |
| [&#x200B; Criteria &#x200B;](https://developer.adobe.com/target/administer/recommendations-api/#tag/Criteria) | Lijst en krijg criteria. |
| [&#x200B; Ontwerpen &#x200B;](https://developer.adobe.com/target/administer/recommendations-api/#tag/Designs) | Ontwerp weergeven, maken, ophalen, bewerken, verwijderen en valideren. |
| [&#x200B; Entiteiten &#x200B;](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities) | Entiteiten opslaan, verwijderen en ophalen. |
| [&#x200B; Bevorderingen &#x200B;](https://developer.adobe.com/target/administer/recommendations-api/#tag/Promotions) | Promoties aanbieden, maken, ophalen, bewerken en verwijderen. |
| [&#x200B; Criteria van de Categorie &#x200B;](https://developer.adobe.com/target/administer/recommendations-api/#tag/Category-Criteria) | Categoriecriteria weergeven, maken, ophalen, bewerken en verwijderen. |
| [&#x200B; Criteria van de Douane &#x200B;](https://developer.adobe.com/target/administer/recommendations-api/#tag/Custom-Criteria) | Aangepaste criteria weergeven, maken, ophalen, bewerken en verwijderen. |
| [&#128279;](https://developer.adobe.com/target/administer/recommendations-api/#tag/Item-Criteria) Criteria van 0&rbrace; Punt | Objectcriteria weergeven, maken, ophalen, bewerken en verwijderen. |
| [&#x200B; Popularity Criteria &#x200B;](https://developer.adobe.com/target/administer/recommendations-api/#tag/Popularity-Criteria) | Maak een lijst, maak, krijg, bewerk en verwijder populiteitscriteria. |
| [&#x200B; Criteria van het Attribuut van het Profiel &#x200B;](https://developer.adobe.com/target/administer/recommendations-api/#tag/Profile-Attribute-Criteria) | Criteria voor profielkenmerken weergeven, maken, ophalen, bewerken en verwijderen. |
| [&#x200B; Recente Criteria &#x200B;](https://developer.adobe.com/target/administer/recommendations-api/#tag/Recent-Criteria) | Recente criteria weergeven, maken, ophalen, bewerken en verwijderen. |
| [&#x200B; Criteria van de Opeenvolging &#x200B;](https://developer.adobe.com/target/administer/recommendations-api/#tag/Sequence-Criteria) | U kunt volgreekscriteria weergeven, maken, ophalen, bewerken en verwijderen. |

## Referentiedocumentatie

* [Adobe Target Delivery API-documentatie](/help/dev/implement/delivery-api/overview.md)
* [&#x200B; integreer Aanbevelingen met e-mail &#x200B;](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/integrating-recs-email.html?lang=nl-NL)

## Samenvatting en revisie

Gefeliciteerd! Door deze gids in te vullen, hebt u geleerd hoe te:
* [Uw catalogus beheren met de API voor aanbevelingen](manage-catalog.md)
* [Aangepaste criteria beheren met de API voor aanbevelingen](manage-custom-criteria.md)
* [De leverings-API gebruiken met aanbevelingen](fetch-recs-server-side-delivery-api.md)
