---
keywords: Recommendations, instellingen, voorkeuren, industrie verticaal, filterincompatibele criteria, standaard hostgroep, duimbasis url, aanbevelingen api token, $9
description: Leer hoe u implementeert [!UICONTROL Recommendations] activiteiten in [!DNL Adobe Target].
title: Hoe implementeren [!UICONTROL Recommendations] Activiteiten?
feature: Recommendations
exl-id: af1e8b60-6dbb-451b-aa4f-e167d1800d1c
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '1403'
ht-degree: 0%

---

# Plan en implementeer [!UICONTROL Recommendations]

Informatie om u te helpen plannen en uitvoeren [!DNL Adobe Target Recommendations].

>[!NOTE]
>
>Naast dit artikel [Adobe Target Business Practice Guide](https://experienceleague.adobe.com/docs/target/using/target-home.html){target=_blank} contains in-depth information about [Target Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html){target=_blank}.

Voordat u de eerste instelt [!UICONTROL Recommendations] activiteit in [!DNL Adobe Target]Voer de volgende stappen uit:

1. [Implementeren [!UICONTROL Target]](#implement-target) op het web en in mobiele apps die u wilt gebruiken voor het vastleggen van gebruikersgedrag en het doen van aanbevelingen.
1. [Stel uw [!UICONTROL Recommendations] catalogus](#set-up-your-recommendations-catalog) van producten of inhoud die u aan uw gebruikers wilt aanbevelen.
1. [Gedragsinformatie en context doorgeven](#pass-behavioral-information-and-context) tot [!DNL Target Recommendations] om het in staat te stellen gepersonaliseerde aanbevelingen te doen.
1. [Algemene uitsluitingen configureren](#configure-global-exclusions).
1. [Configureren [!UICONTROL Recommendations] instellingen](#configure-recommendations-settings).
1. (Optioneel) [Beheren [!UICONTROL Recommendations] Admin API&#39;s gebruiken](#administer-recommendations-using-admin-apis).

## 1. Uitvoeren [!UICONTROL Target]

[!DNL Target Recommendations] vereist dat u de SDK van het Web van Adobe Experience Platform of in.js 0.9.2 (of later) uitvoert. Zie de [[!UICONTROL Target] implementatiehandleidingen op de client](../client-side/overview.md) voor meer informatie .

## 2. Stel uw [!UICONTROL Recommendations] catalogus

Om aanbevelingen van hoge kwaliteit te doen, [!UICONTROL Target] moet weten welke producten of inhoud u wilt aanbevelen. Catalogi bevatten doorgaans drie typen informatie over aanbevolen items. Stel dat u films aanbeveelt. Neem het volgende op:

1. Gegevens die u aan de gebruiker wilt tonen die de aanbeveling ontvangt. U kunt bijvoorbeeld de naam van de film en een URL voor een miniatuurafbeelding van de filmposter weergeven.
1. Gegevens die nuttig zijn voor het toepassen van marketing- en verkoopbesturingselementen. U kunt bijvoorbeeld de classificatie van de film weergeven, zodat u geen NC-17-films aanbeveelt.
1. Gegevens die nuttig zijn om de gelijkenis van items met andere items te bepalen. U kunt bijvoorbeeld het genre van de film en de filmdirecteur weergeven.

[!UICONTROL Target] bevat meerdere integratieopties om uw catalogus te vullen. Deze opties kunnen in combinatie worden gebruikt om verschillende items in de catalogus bij te werken of om verschillende itemkenmerken op verschillende frequenties bij te werken.

| Methode | Wat het is | Wanneer gebruikt u het | Aanvullende informatie |
| --- | --- | --- | --- |
| Catalogusfeed | Plan een feed (CSV, Google Product XML of Analytics Product Classifications) die dagelijks moet worden geüpload en opgenomen. | Voor het verzenden van informatie over meerdere items tegelijk. Voor het verzenden van informatie die niet vaak wordt gewijzigd. | Zie [Feeds](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html). |
| Entiteiten-API | Roep API aan om updates naar de minuut voor één enkel punt te verzenden. | Voor het verzenden van updates zoals deze over één item tegelijk plaatsvinden. Voor het verzenden van informatie die regelmatig verandert (bijvoorbeeld prijs, voorraad/voorraadniveau). | Zie de [Documentatie voor ontwikkelaars van Entiteiten-API](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities). |
| Updates op de pagina doorgeven | Updates voor één item verzenden met JavaScript op de pagina of met de API voor levering. | Voor het verzenden van updates zoals deze over één item tegelijk plaatsvinden. Voor het verzenden van informatie die regelmatig verandert (bijvoorbeeld prijs, voorraad/voorraadniveau). | Zie [Objectweergaven/productpagina&#39;s](#item-views-or-product-pages) hieronder. |

De meeste klanten zouden minstens één voer moeten uitvoeren. Vervolgens kunt u ervoor kiezen om uw feed aan te vullen met updates voor vaak gewijzigde kenmerken of items met behulp van de Entities API of de on-the-page methode.

## 3. Gedragsinformatie en context doorgeven

De gedragsinformatie en de context die u moet doorgeven [!UICONTROL Target] is afhankelijk van de actie die de bezoeker uitvoert. Dit is vaak afhankelijk van het type pagina waarmee de bezoeker communiceert.

### Objectweergaven of productpagina&#39;s

Op pagina&#39;s waarop een bezoeker één item weergeeft, zoals een pagina met productdetails, moet u de identiteit doorgeven van het item dat de bezoeker bekijkt. U zou ook de korrelste categorie van het punt moeten overgaan dat de bezoeker bekijkt, om het filtreren aanbevelingen aan de huidige categorie toe te staan.

U kunt ook bepaalde snel veranderende kenmerken op de productpagina zelf doorgeven. U kunt bijvoorbeeld de prijs doorgeven (`value`) en voorraadniveau.

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

Op een winkelwagentje kunt u objecten aanbevelen op basis van de inhoud van het huidige winkelwagentje van de bezoeker. Geef hiertoe de id&#39;s van alle items in het huidige winkelwagentje van de bezoeker door met behulp van de speciale parameter `cartIds`.

#### Items die momenteel in winkelwagentje staan doorgeven

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "cartIds": "352,223,23432,432,553"
      }
}
```

Zie voor meer informatie over op winkelwagentjes gebaseerde aanbevelingen [Op basis van winkelwagentje](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based) in de *[!DNL Adobe Target]Handelspraktijken*.

### Objecten uitsluiten die al in de winkelwagentje van de bezoeker staan

Op pagina&#39;s op de hele site kunt u bepaalde items uitsluiten van aanbevelingen. U kunt bijvoorbeeld items die zich al in het huidige winkelwagentje van de bezoeker bevinden, niet aanbevelen. Geef daartoe de id&#39;s door van alle items die u wilt uitsluiten met behulp van de speciale parameter `excludedIds`.

#### Items doorgeven die moeten worden uitgesloten

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "excludedIds": "352,223,23432,432,553"
      }
}
```

### Pagina&#39;s voor kopen/bestellen bevestigen

Wanneer een aankoopgebeurtenis plaatsvindt, geeft u de identiteit door van het gekochte item of de gekochte items. Zie [Conversies bijhouden](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions) in de [Hoe te om bij.js uit te voeren > uitvoeren [!UICONTROL Target] zonder tagbeheer](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md) artikel.

## 4. Algemene uitsluitingen configureren

Sluit items op algemeen niveau uit die u nooit aan een bezoeker wilt aanbevelen. Zie [Uitsluitingen](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/exclusions.html) in de *[!DNL Adobe Target]Handelspraktijken*.

## 5. Configureren [!UICONTROL Recommendations] instellingen

Instellingen gebruiken om uw [!UICONTROL Recommendations] uitvoering.

Als u toegang wilt krijgen tot **[!UICONTROL Recommendations Settings]** opties, opent u Doel in de [!DNL Adobe Experience Cloud]en klik vervolgens op **[!UICONTROL Recommendations]** > **[!UICONTROL Settings]**.

![alternatieve afbeelding](assets/recs_settings.png)

De volgende opties zijn beschikbaar:

| Instelling | Beschrijving |
|--- |--- |
| Aangepaste globale mabox | (Optioneel) Geef de aangepaste globale box op die wordt gebruikt voor de server [!UICONTROL Target] activiteiten. Standaard wordt de algemene box gebruikt door [!UICONTROL Target] wordt gebruikt voor [!UICONTROL Recommendations].<P>Opmerking: deze optie is ingesteld op het tabblad [!UICONTROL Target] **[!UICONTROL Administration]** pagina. Openen [!UICONTROL Target]en klik vervolgens op **[!UICONTROL Administration]** > **[!UICONTROL Visual Experience Composer]**. |
| Verticale industrie | De industrie verticaal wordt gebruikt helpen uw aanbevelingen criteria categoriseren. Deze informatie helpt leden van uw team criteria te vinden die voor een bepaalde pagina, zoals criteria zinvol zijn die voor de het winkelwagentje pagina of voor een media pagina het best zijn. |
| Niet-compatibele criteria filteren | Schakel deze optie in om alleen die criteria weer te geven waarbij de geselecteerde pagina de vereiste gegevens doorgeeft. Niet alle criteria worden op elke pagina correct uitgevoerd. De pagina of het selectievakje moet worden ingeschakeld `entity.id` of `entity.categoryId` voor het huidige item/de huidige categorie-aanbevelingen compatibel te maken. Over het algemeen is het beter alleen compatibele criteria te laten zien. Schakel deze optie echter uit als u incompatibele criteria voor de activiteit wilt gebruiken.<P>U wordt aangeraden deze optie uit te schakelen als u een oplossing voor tagbeheer gebruikt.<P>Zie voor meer informatie over deze optie [[!UICONTROL Recommendations] Veelgestelde vragen](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html) in de *[!DNL Adobe Target]Handelspraktijken*. |
| Standaardhostgroep | Selecteer de standaardhostgroep.<P>U kunt de hostgroep gebruiken om de beschikbare items in uw catalogus te scheiden voor verschillende toepassingen. U kunt bijvoorbeeld hostgroepen gebruiken voor ontwikkelings- en productieomgevingen, verschillende merken of verschillende geografische locaties. Standaard zijn de voorvertoningsresultaten in Cataloguszoekopdrachten, Verzamelingen en Uitsluitingen gebaseerd op de standaardhostgroep. (U kunt ook een andere hostgroep selecteren om een voorvertoning van de resultaten weer te geven met behulp van het filter Omgeving.) Nieuwe toegevoegde items zijn standaard beschikbaar in alle hostgroepen, tenzij een milieu-id is opgegeven bij het maken of bijwerken van het item. De geleverde aanbevelingen hangen van de gastheergroep af die in het verzoek wordt gespecificeerd.<P>Als u uw producten niet ziet, zorg ervoor dat u de correcte gastheergroep gebruikt. Bijvoorbeeld, als u opstelling uw aanbeveling om een het opvoeren milieu te gebruiken en u uw gastheergroep aan het Opvoeren plaatst, zou u uw inzamelingen in het opvoeren milieu voor de te tonen producten kunnen moeten opnieuw creëren. Als u wilt zien welke producten in elke omgeving beschikbaar zijn, gebruikt u Cataloguszoekopdracht voor elke omgeving. U kunt ook een voorvertoning weergeven van de inhoud van [!UICONTROL Recommendations] verzamelingen en uitsluitingen voor een geselecteerde omgeving (hostgroep).<P>**Opmerking:** Nadat u de geselecteerde omgeving hebt gewijzigd, moet u op Zoeken klikken om de geretourneerde resultaten bij te werken.<P> **[!UICONTROL The Environment]** is beschikbaar op de volgende plaatsen in het Doel UI:<ul><li>Catalogus zoeken (**[!UICONTROL Recommendations]** > **[!UICONTROL Catalog Search]**)</li><li>Verzameling maken, dialoogvenster (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Create New]**)</li><li>Het dialoogvenster Verzameling bijwerken (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Edit]**)</li><li>Dialoogvenster Uitsluiting maken (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Create New]**)</li><li>Dialoogvenster Uitsluiting bijwerken (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Edit]**)</li></ul>Zie voor meer informatie [Gastheren](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) in de *[!DNL Adobe Target]Handelspraktijken*. |
| Basis-URL miniatuur | Als u een basis-URL instelt voor uw productcatalogus, kunt u relatieve URL&#39;s gebruiken wanneer u miniaturen van uw producten opgeeft wanneer u de URL van de miniatuur doorgeeft.<P>Bijvoorbeeld:<P>`"entity.thumbnailURL=/Images/Homepage/product1.jpg"`<P>Hiermee stelt u een URL in ten opzichte van de basis-URL van de miniatuur. |
| [!UICONTROL Recommendations] API-token | Deze token gebruiken in [!UICONTROL Recommendations] API-aanroepen, zoals de API voor downloaden. |

## 6. (Optioneel) Beheren [!UICONTROL Recommendations] Admin API&#39;s gebruiken

Zie de [Gebruiken [!UICONTROL Recommendations] API&#39;s](../../before-administer/recs-api/overview.md) hands-on gids leren om te vormen en te gebruiken [!UICONTROL Target] API&#39;s voor beheer en levering voor [!UICONTROL Recommendations].
