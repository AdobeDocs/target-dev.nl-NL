---
keywords: Aanbevelingen, instellingen, voorkeuren, industrie verticaal, filtercriteria, standaard hostgroep, duimbasis-url, aanbevelingen api-token, $9
description: Leer hoe u [!UICONTROL Recommendations] -activiteiten implementeert in  [!DNL Adobe Target] .
title: Hoe kan ik [!UICONTROL Recommendations] -activiteiten implementeren?
feature: Recommendations
exl-id: af1e8b60-6dbb-451b-aa4f-e167d1800d1c
source-git-commit: 94a4122244065384f487ca9a29dfa1b414168cb8
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 0%

---

# Plan en implementeer [!UICONTROL Recommendations]

Informatie die u helpt bij het plannen en implementeren van [!DNL Adobe Target Recommendations] .

>[!NOTE]
>
>Naast dit artikel, bevat de [ Gids Van Bedrijfs Adobe Target van de Praktijk ](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=nl-NL){target=_blank} diepgaande informatie over [ Aanbevelingen van het Doel ](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html?lang=nl-NL){target=_blank}.

Voer de volgende stappen uit voordat u de eerste [!UICONTROL Recommendations] activiteit in [!DNL Adobe Target] instelt:

1. [ voer [!UICONTROL Target]](#implement-target) op het Web en mobiele toepassingsoppervlakken uit die u voor het vangen van gebruikersgedrag en het leveren van aanbevelingen wilt gebruiken.
1. [ Opstelling uw [!UICONTROL Recommendations] catalogus ](#set-up-your-recommendations-catalog) van producten of inhoud die u aan uw gebruikers wilt adviseren.
1. [ ga gedragsinformatie en context ](#pass-behavioral-information-and-context) tot [!DNL Target Recommendations] over om het toe te staan om gepersonaliseerde aanbevelingen te leveren.
1. [ vorm globale uitsluitingen ](#configure-global-exclusions).
1. [ vorm [!UICONTROL Recommendations] montages ](#configure-recommendations-settings).
1. (Facultatief) [ beheert [!UICONTROL Recommendations] gebruikend Admin APIs ](#administer-recommendations-using-admin-apis).

## &#x200B;1. Implementeren [!UICONTROL Target]

[!DNL Target Recommendations] vereist dat u de Adobe Experience Platform Web SDK of at.js 0.9.2 (of hoger) implementeert. Zie de [[!UICONTROL Target] cliënt-zijimplementatiegidsen ](../client-side/overview.md) voor meer informatie.

## &#x200B;2. Stel de catalogus [!UICONTROL Recommendations] in

[!UICONTROL Target] moet weten welke producten of inhoud u wilt aanbevelen om aanbevelingen van hoge kwaliteit te kunnen uitvoeren. Catalogi bevatten doorgaans drie typen informatie over aanbevolen items. Stel dat u films aanbeveelt. Neem het volgende op:

1. Gegevens die u aan de gebruiker wilt tonen die de aanbeveling ontvangt. U kunt bijvoorbeeld de naam van de film en een URL voor een miniatuurafbeelding van de filmposter weergeven.
1. Gegevens die nuttig zijn voor het toepassen van marketing- en verkoopbesturingselementen. U kunt bijvoorbeeld de classificatie van de film weergeven, zodat u geen NC-17-films aanbeveelt.
1. Gegevens die nuttig zijn om de gelijkenis van items met andere items te bepalen. U kunt bijvoorbeeld het genre van de film en de filmdirecteur weergeven.

[!UICONTROL Target] biedt meerdere integratieopties om uw catalogus te vullen. Deze opties kunnen in combinatie worden gebruikt om verschillende items in de catalogus bij te werken of om verschillende itemkenmerken op verschillende frequenties bij te werken.

| Methode | Wat het is | Wanneer gebruikt u het | Aanvullende informatie |
| --- | --- | --- | --- |
| Catalogusfeed | Plan een feed (CSV, Google Product XML of Analytics Product Classifications) die dagelijks moet worden geüpload en opgenomen. | Voor het verzenden van informatie over meerdere items tegelijk. Voor het verzenden van informatie die niet vaak wordt gewijzigd. | Zie [ Eigen voer ](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html?lang=nl-NL). |
| Entiteiten-API | Roep API aan om updates naar de minuut voor één enkel punt te verzenden. | Voor het verzenden van updates zoals deze over één item tegelijk plaatsvinden. Voor het verzenden van informatie die regelmatig verandert (bijvoorbeeld prijs, voorraad/voorraadniveau). | Zie [ de ontwikkelaarsdocumentatie van Entiteiten API ](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities). |
| Updates op de pagina doorgeven | Updates voor één item verzenden met JavaScript op de pagina of met de leverings-API. | Voor het verzenden van updates zoals deze over één item tegelijk plaatsvinden. Voor het verzenden van informatie die regelmatig verandert (bijvoorbeeld prijs, voorraad/voorraadniveau). | Zie [ meningen van het Punt/productpagina&#39;s ](#item-views-or-product-pages) hieronder. |

>[!IMPORTANT]
>
>Wees voorzichtig wanneer u [!DNL Recommendations] [!UICONTROL Catalog] via [!DNL Delivery API] bijwerkt. Het bestand [!DNL Delivery API] is public, gebruik dit dus niet om klikbare items in de catalogus met aanbevelingen te vullen. Zo kunt u ongeldig inhoud introduceren en uw catalogus vervuilen.
>
>**Beste praktijken**: Gebruik [!DNL Delivery API] slechts voor het bijwerken van catalogusattributen die:
>
>* Verandering regelmatig (bijvoorbeeld prijs, voorraadniveau).
>
>* Volg een vooraf gedefinieerde indeling die gemakkelijk op uw website kan worden gevalideerd.
>
>* Gebruik deze optie niet voor het toevoegen of wijzigen van klikbare items of andere niet-geverifieerde inhoud.
>
>* Indien nodig kunt u klantenondersteuning aanvragen om catalogusupdates uit te schakelen via de bezorgings-API.
>
>Zie de [[!UICONTROL Adobe Target Delivery API] ](https://developer.adobe.com/target/implement/delivery-api/){target=_blank} documentatie voor meer informatie.

De meeste klanten zouden minstens één voer moeten uitvoeren. Vervolgens kunt u ervoor kiezen om uw feed aan te vullen met updates voor vaak gewijzigde kenmerken of items met behulp van de Entities API of de on-the-page methode.

## &#x200B;3. Gedragsinformatie en context doorgeven

De gedragsinformatie en de context die u aan [!UICONTROL Target] moet doorgeven, zijn afhankelijk van de actie die uw bezoeker uitvoert. Deze actie is vaak gekoppeld aan het type pagina waarmee uw bezoeker communiceert.

### Objectweergaven of productpagina&#39;s

Op pagina&#39;s waarop een bezoeker één item weergeeft, zoals een pagina met productdetails, moet u de identiteit doorgeven van het item dat de bezoeker bekijkt. U zou ook de korrelste categorie van het punt moeten overgaan dat de bezoeker bekijkt, om het filtreren aanbevelingen aan de huidige categorie toe te staan.

U kunt ook bepaalde snel veranderende kenmerken op de productpagina zelf doorgeven. U kunt bijvoorbeeld de prijs (`value`) en voorraad-/voorraadniveau doorgeven.

#### Voldoende prijs en voorraad

```js {line-numbers="true"}
<script type="text/javascript">
function targetPageParams() { 
   return { 
      "entity": { 
         "id": "32323", 
         "categoryId": "running-shoes", 
         "value": 119.99, 
         "inventory": 329 
      } 
   } 
}
</script>
```

### Categorieweergaven/categoriepagina&#39;s

Op een categoriepagina wilt u waarschijnlijk uw aanbevelingen beperken tot producten of inhoud binnen die categorie. Hiervoor moet u de identiteit van de momenteel weergegeven categorie doorgeven.

#### Huidige categorie doorgeven

```js {line-numbers="true"}
function targetPageParams() { 
   return { 
      "entity": { 
         "categoryId": "running-shoes" 
      } 
   } 
}
```

### Winkelwagentweergaven/winkelwagentjes/afhandelingspagina&#39;s

Op een winkelwagentje kunt u objecten aanbevelen op basis van de inhoud van het huidige winkelwagentje van de bezoeker. Geef hiertoe de id&#39;s van alle items in het huidige winkelwagentje van de bezoeker door met de speciale parameter `cartIds` .

#### Items die momenteel in winkelwagentje staan doorgeven

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "cartIds": "352,223,23432,432,553"
      }
}
```

Voor meer informatie over op kunst-Gebaseerde aanbevelingen, zie [ op kunst-Gebaseerde ](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=nl-NL#cart-based) in de *[!DNL Adobe Target]Gids Bedrijfs van de Praktijk*.

### Objecten uitsluiten die al in de winkelwagentje van de bezoeker staan

Op pagina&#39;s op de hele site kunt u bepaalde items uitsluiten van aanbevelingen. U kunt bijvoorbeeld items die zich al in het huidige winkelwagentje van de bezoeker bevinden, niet aanbevelen. Geef hiertoe de id&#39;s door van alle items die u wilt uitsluiten met de speciale parameter `excludedIds` .

#### Items doorgeven die moeten worden uitgesloten

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "excludedIds": "352,223,23432,432,553"
      }
}
```

### Pagina&#39;s voor kopen/bestellen bevestigen

Wanneer een aankoopgebeurtenis plaatsvindt, geeft u de identiteit door van het gekochte item of de gekochte items. Zie [ Conversies van het Spoor ](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions) in [ hoe te om at.js uit te voeren > [!UICONTROL Target] zonder een artikel van de markeringsmanager ](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md) uitvoert.

## &#x200B;4. Algemene uitsluitingen configureren

Sluit items op algemeen niveau uit die u nooit aan een bezoeker wilt aanbevelen. Zie [ Uitsluitingen ](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/exclusions.html?lang=nl-NL) in de *[!DNL Adobe Target]Gids Bedrijfs van de Praktijk*.

## &#x200B;5. Configureer [!UICONTROL Recommendations] -instellingen

Gebruik instellingen om uw [!UICONTROL Recommendations] -implementatie te beheren.

Als u de opties van **[!UICONTROL Recommendations Settings]** wilt openen, opent u Doel in [!DNL Adobe Experience Cloud] en klikt u op **[!UICONTROL Recommendations]** > **[!UICONTROL Settings]** .

![ pagina van de Montages van Aanbevelingen ](/help/dev/implement/recommendations/assets/recs_settings.png)

De volgende opties zijn beschikbaar:

| Instelling | Beschrijving |
|--- |--- |
| Aangepaste globale mabox | (Optioneel) Geef de aangepaste globale box op die wordt gebruikt voor [!UICONTROL Target] -activiteiten. Standaard wordt de algemene box die door [!UICONTROL Target] wordt gebruikt, gebruikt voor [!UICONTROL Recommendations] .<P>Opmerking: deze optie wordt ingesteld op de pagina [!UICONTROL Target] **[!UICONTROL Administration]** . Open [!UICONTROL Target] en klik vervolgens op **[!UICONTROL Administration]** > **[!UICONTROL Visual Experience Composer]** . |
| Verticale industrie | De industrie verticaal wordt gebruikt helpen uw aanbevelingen criteria categoriseren. Deze informatie helpt leden van uw team criteria te vinden die voor een bepaalde pagina, zoals criteria zinvol zijn die voor de het winkelwagentje pagina of voor een media pagina het best zijn. |
| Niet-compatibele criteria filteren | Schakel deze optie in om alleen die criteria weer te geven waarbij de geselecteerde pagina de vereiste gegevens doorgeeft. Niet alle criteria worden op elke pagina correct uitgevoerd. De pagina of het kader moet `entity.id` of `entity.categoryId` doorgeven om de huidige aanbevelingen voor het item of de huidige categorie compatibel te maken. Over het algemeen is het beter alleen compatibele criteria te laten zien. Schakel deze optie echter uit als u incompatibele criteria voor de activiteit wilt gebruiken.<P>U wordt aangeraden deze optie uit te schakelen als u een oplossing voor tagbeheer gebruikt.<P>Voor meer informatie over deze optie, zie [[!UICONTROL Recommendations] Veelgestelde vragen ](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=nl-NL) in de *[!DNL Adobe Target]Gids Bedrijfs van de Praktijk*. |
| Standaardhostgroep | Selecteer de standaardhostgroep.<P>U kunt de hostgroep gebruiken om de beschikbare items in uw catalogus te scheiden voor verschillende toepassingen. U kunt bijvoorbeeld hostgroepen gebruiken voor ontwikkelings- en productieomgevingen, verschillende merken of verschillende geografische locaties. Standaard zijn de voorvertoningsresultaten in Cataloguszoekopdrachten, Verzamelingen en Uitsluitingen gebaseerd op de standaardhostgroep. (U kunt ook een andere hostgroep selecteren om een voorvertoning van de resultaten weer te geven met behulp van het filter Omgeving.) Nieuwe toegevoegde items zijn standaard beschikbaar in alle hostgroepen, tenzij een milieu-id is opgegeven bij het maken of bijwerken van het item. De geleverde aanbevelingen hangen van de gastheergroep af die in het verzoek wordt gespecificeerd.<P>Als u uw producten niet ziet, zorg ervoor dat u de correcte gastheergroep gebruikt. Bijvoorbeeld, als u opstelling uw aanbeveling om een het opvoeren milieu te gebruiken en u uw gastheergroep aan het Opvoeren plaatst, zou u uw inzamelingen in het opvoeren milieu voor de te tonen producten kunnen moeten opnieuw creëren. Als u wilt zien welke producten in elke omgeving beschikbaar zijn, gebruikt u Cataloguszoekopdracht voor elke omgeving. U kunt ook een voorvertoning weergeven van de inhoud van [!UICONTROL Recommendations] -verzamelingen en -uitsluitingen voor een geselecteerde omgeving (hostgroep).<P>**Nota:** na het veranderen van het geselecteerde milieu, moet u Onderzoek klikken om de teruggekeerde resultaten bij te werken.<P> **[!UICONTROL The Environment]** -filter is beschikbaar op de volgende plaatsen in de interface van het doel:<ul><li>Catalogus zoeken (**[!UICONTROL Recommendations]** > **[!UICONTROL Catalog Search]**)</li><li>Dialoogvenster Verzameling maken (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Create New]**)</li><li>Dialoogvenster Verzameling bijwerken (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Edit]**)</li><li>Dialoogvenster Uitsluiting maken (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Create New]**)</li><li>Dialoogvenster Uitsluiting bijwerken (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Edit]**)</li></ul>Voor meer informatie, zie [ Gastheren ](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=nl-NL) in de *[!DNL Adobe Target]Gids Bedrijfs van de Praktijk*. |
| Basis-URL miniatuur | Als u een basis-URL instelt voor uw productcatalogus, kunt u relatieve URL&#39;s gebruiken wanneer u miniaturen van uw producten opgeeft wanneer u de URL van de miniatuur doorgeeft.<P>Bijvoorbeeld:<P>`"entity.thumbnailURL=/Images/Homepage/product1.jpg"`<P>Hiermee stelt u een URL in ten opzichte van de basis-URL van de miniatuur. |
| [!UICONTROL Recommendations] API-token | Gebruik dit token in API-aanroepen van [!UICONTROL Recommendations] , zoals de API voor downloaden. |

## &#x200B;6. (Optioneel) Beheer [!UICONTROL Recommendations] met API&#39;s voor beheerders

Zie het [ Gebruik [!UICONTROL Recommendations] APIs ](../../before-administer/recs-api/overview.md) hands-on gids om te leren hoe te om [!UICONTROL Target] admin en levering APIs voor [!UICONTROL Recommendations] te vormen en te gebruiken.
