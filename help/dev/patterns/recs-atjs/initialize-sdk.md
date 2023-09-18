---
title: SDK's initialiseren
description: Zorg ervoor dat alle noodzakelijke stappen voor het laden van de [!DNL Adobe Target] JavaScript-bibliotheek at.js wordt in de juiste volgorde uitgevoerd.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: a87f9a13fc1feb12c62f1b772975958541f7523a
workflow-type: tm+mt
source-wordcount: '1708'
ht-degree: 0%

---

# SDK&#39;s initialiseren

Voer de stappen in het dialoogvenster *SDK initialiseren* diagram om ervoor te zorgen dat alle noodzakelijke taken nodig zijn om het [!DNL Adobe Target] JavaScript-bibliotheek at.js wordt in de juiste volgorde uitgevoerd.

>[!TIP]
>
>Klik op de afbeeldingen in dit onderwerp om het scherm in te vouwen.

## SDKs-diagram initialiseren {#diagram}

Voor toepassingen met meerdere pagina&#39;s vindt deze stroom elke keer dat de pagina opnieuw wordt geladen of dat de bezoeker naar een nieuwe pagina op de website navigeert.

De stapnummers in de volgende afbeelding komen overeen met de onderstaande secties.

![SDKs-diagram initialiseren](/help/dev/patterns/recs-atjs/assets/diagram-initiaze-sdk.png){width="600" zoomable="yes"}

Klik op de volgende koppelingen om naar de gewenste secties te navigeren:

* [1.1: SDK van de API voor bezoekers laden](#load)
* [1.2: Klantnummer instellen](#set)
* [1.3: automatische aanvraag voor het laden van pagina&#39;s configureren](#automatic)
* [1.4: Flikkerverwerking configureren](#flicker)
* [1.5: Gegevenstoewijzing configureren](#data-mapping)
* [1.6. Promotie](#promotion)
* [1.7: op auto&#39;s gebaseerde criteria](#cart)
* [1.8: criteria op basis van populariteit](#popularity)
* [1.9: Objectcriteria](#item)
* [1.10: Gebruikerscriteria](#user)
* [1.11: Aangepaste criteria](#custom)
* [1.12: Vermeld de kenmerken die in de opnemingsregels worden gebruikt](#inclusion)
* [1.13: Uitgesloten id&#39;s verstrekken](#exclude)
* [1.14: Geef de parameter entity.event.detailsOnly=true door](#true)
* [1.15: Externe gegevenstoewijzing configureren](#remote)
* [1.16: Belasting bij.js](#web)

## 1.1: SDK van de API voor bezoekers laden {#load}

Deze stap helpt ervoor te zorgen dat de `VisitorAPI.js` de bibliotheek is correct geladen, geconfigureerd en geïnitialiseerd.

+++Zie details

![SDK-diagram voor Bezoeker-API laden](/help/dev/patterns/recs-atjs/assets/load-visitor-combined.png){width="400" zoomable="yes"}

**Vereisten**

* Als u de Bezoeker-id/API-service wilt gebruiken, moet uw bedrijf zijn ingeschakeld voor de [!DNL Adobe Experience Cloud] en een [!UICONTROL Organization ID]. Zie voor meer informatie [Vereisten voor Experience Cloud: organisatie-id](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html?){target=_blank} in de *Help bij Identiteitsservice* hulplijn.
* U hebt de `VisitorAPI.js` bestand. U moet dit bestand al hebben als u [!DNL Adobe Analytics] geïmplementeerd. Dit bestand kan ook worden toegevoegd via het dialoogvenster [[!DNL Adobe Experience Platform] extensie tags](https://experienceleague.adobe.com/docs/tags.html){target=_blank} or can be downloaded from the [Adobe Analytics Code Manager](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html){target=_blank}.

**Bezoeker API.js configureren en doorverwijzen**

Zie voor meer informatie [Voer de Dienst van het Experience Cloud voor Doel uit](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html){target=_blank}.

**Leesingen**

* [Overzicht van Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html){target=_blank}
* [Over de id-service](https://experienceleague.adobe.com/docs/id-service/using/intro/about-id-service.html){target=_blank}
* [Cookies en de identiteitsservice van Experiencen Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html){target=_blank}
* [Hoe de Dienst van de Identiteit van het Experience Cloud verzoekt en identiteitskaart plaatst](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html){target=_blank}
* [ID-synchronisatie en overeenkomende snelheden](https://experienceleague.adobe.com/docs/id-service/using/intro/match-rates.html){target=_blank}

**Handelingen**

* De `VisitorAPI.js` op uw webpagina&#39;s.
* Meer informatie over de [beschikbare configuraties voor de Bezoeker-id/API-service](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html){target=_blank}.
* Na de `VisitorAPI.js` bestand is geladen, gebruikt u de `Visitor.getInstance` methode om te initialiseren gebruikend de noodzakelijke configuraties u wenst.
* Verken uzelf met de [beschikbare methoden](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html){target=_blank}.

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 1.2: Klantnummer instellen {#set}

Deze stap helpt ervoor te zorgen dat de bekende id&#39;s van uw bezoekers (CRM-id, gebruikersnaam enzovoort) zijn gekoppeld aan de anonieme id van [!DNL Adobe] voor aanpassen naar andere apparaten.

+++Zie details

![Klant-id instellen](/help/dev/patterns/recs-atjs/assets/set-customer-id-combined.png){width="400" zoomable="yes"}

**Vereisten**

* De bekende id van de bezoeker moet beschikbaar zijn in de gegevenslaag.

**Klant-id instellen**
Zie voor meer informatie [setCustomerIDs](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html){target=_blank}.

**Leesingen**

* [Real-time profielsynchronisatie voor mbox3rdPartyId](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html){target=_blank}

**Handelingen**

* Gebruiken `visitor.setCustomerIDs` om de bekende id van de bezoeker in te stellen.

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 1.3: Een automatische aanvraag voor het laden van pagina&#39;s configureren {#automatic}

Met deze stap kan at.js alle ervaringen ophalen die op de pagina moeten worden weergegeven tijdens het laden van het JavaScript-bibliotheekbestand at.js.

+++Zie details

![Automatische aanvraag voor het laden van pagina&#39;s configureren](/help/dev/patterns/recs-atjs/assets/configure-automatic-page-request-combined.png){width="400" zoomable="yes"}

**Vereisten**

* Niet alle gegevens in de gegevenslaag moeten worden verzonden naar [!DNL Target]. Overleg met uw bedrijfsteam (het digitale marketing team) om te bepalen welke gegevens voor experimenteren, optimalisering, en verpersoonlijking waardevol zijn. Alleen deze gegevens mogen worden verzonden naar [!DNL Target].
* Zorg ervoor dat u geen PII-gegevens (Personal Identified Information) verzendt naar [!DNL Target].

**Automatische aanvraag voor het laden van pagina&#39;s configureren**

Zie voor meer informatie [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Leesingen**

Meer informatie over de `pageLoadEnabled` instellen in [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Handelingen**

* Wijzig de `window.targetGlobalSettings` -object om automatische aanvragen voor het laden van pagina&#39;s in te schakelen.

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 1.4: Flikkerverwerking configureren {#flicker}

Deze stap helpt ervoor te zorgen dat er geen paginafflikkering is wanneer het leveren van ervaringen.

+++Zie details

![Flikkeringsdiagram configureren](/help/dev/patterns/recs-atjs/assets/flicker-handling-combined.png){width="400" zoomable="yes"}

**Vereisten**

* Heb een bespreking met het team verantwoordelijk voor Webpaginaprestaties betreffende de voor- en nadelen van het controleren van flikkering gebruikend de standaardmethode die door at.js wordt gebruikt. U kunt naar ontwerppatronen zoeken waarmee u aangepaste flikkerafhandelingsoplossing kunt gebruiken, zoals de animatie van de lader. Als u geen patroon vindt, kunt u om een nieuw patroon verzoeken.

**Flickbehandeling configureren**

Zie voor meer informatie [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

Instelling `bodyHidingEnabled` tot `true` Hiermee verbergt u de gehele pagina terwijl de aanvraag voor het laden van de pagina wordt uitgevoerd. Als u de automatische aanvraag voor het laden van pagina&#39;s om welke reden dan ook niet hebt ingeschakeld (gegevens zijn later bijvoorbeeld niet beschikbaar), kunt u deze instelling het beste instellen op `false`.

Als u `bodyHidingEnabled` omdat u APLR niet wilt starten en de paginaaanvraag later wilt doorlopen, of omdat u geen flikkerbehandeling nodig hebt, moet u uw eigen flikkerbehandeling implementeren. U kunt de flikkering op twee manieren verwerken: door de te testen gedeelten te verbergen of door een spuitbus weer te geven op de te testen gedeelten.

**Leesingen**

* [Hoe at.js flikkering beheert](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
* Meer informatie over de objecten bodyHiddenStyle en bodyHidingEnabled in [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Handelingen**

* Wijzig de `window.targetGlobalSettings` in te stellen object `bodyHiddenStyle` en `bodyHidingEnabled`.

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 1.5: Gegevenstoewijzing configureren {#data-mapping}

Deze stap helpt ervoor te zorgen dat alle gegevens die moeten worden verzonden naar [!DNL Target] is ingesteld.

+++Zie details

![Gegevenstoewijzingsdiagram](/help/dev/patterns/recs-atjs/assets/data-mapping-combined.png){width="400" zoomable="yes"}

**Vereisten**

* De gegevenslaag zou met alle gegevens klaar moeten zijn die moeten worden verzonden naar [!DNL Target].
* Recommendations: verrijken profiel.
   * Voldoende `entity.id` gegevens vastleggen voor onlangs bekeken criteria en items op basis van criteria die zijn gebaseerd op het laatst bekeken product.
   * Voldoende `entity.id` gegevens vastleggen voor populiteitscriteria op basis van favoriete categorie.
   * Geef het profielkenmerk door als de aangepaste criteria hierop zijn gebaseerd of worden gebruikt bij het filteren van de inclusieregel in criteria.
* Recommendations: gegevens van ingesloten producten.
   * Andere entiteitsparameters (gereserveerd en aangepast) kunnen worden doorgegeven aan het toevoegen of bijwerken van de productcatalogus in [!DNL Recommendations].
   * De productcatalogus kan ook worden bijgewerkt met behulp van eenheidfeeds met behulp van de [!DNL Target] UI of API.

**Gegevens toewijzen aan[!DNL Target]**

Zie voor meer informatie [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Leesingen**

* [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)
* [Recommendations plannen en implementeren](/help/dev/implement/recommendations/recommendations.md)
* [Een Recommendations-catalogus instellen](/help/dev/implement/recommendations/recommendations.md)

**Handelingen**

* Gebruik de `targetPageParams()` functie om alle vereiste gegevens in te stellen waarnaar moet worden verzonden [!DNL Target].

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 1.6. Promotie {#promotion}

Aanbevolen objecten toevoegen en de plaatsing ervan in uw [!DNL Target Recommendations] [ontwerpen](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++Zie details

**Beschikbare opties**

* Promoten met id&#39;s
* [Bevorderen per collectie](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Promoten op kenmerk](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Vereiste parameters voor entiteit**

* Het kenmerk Item in de speciale actie moet worden doorgegeven wanneer de optie &#39;Promoten door kenmerk&#39; wordt gebruikt.

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 1.7: op auto&#39;s gebaseerde criteria {#cart}

Aanbevelingen doen op basis van de inhoud van het winkelwagentje.

+++Zie details

**Beschikbare criteria**

* [!UICONTROL People Who Viewed These, Viewed Those]
* [!UICONTROL People Who Viewed These, Bought Those]
* [!UICONTROL People Who Bought These, Bought Those]

**Vereiste parameters voor entiteit**

* cartIds

**Leesingen**

* [Op basis van winkelwagentje](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 1.8: criteria op basis van populariteit {#popularity}

Aanbevelingen doen op basis van de algemene populariteit van een item op uw site of op basis van de populariteit van items in de favoriete of meest bekeken categorie, het merk, het genre enzovoort van een gebruiker.

+++Zie details

**Beschikbare criteria**

* [!UICONTROL Most Viewed Across the Site]
* [!UICONTROL Most Viewed by Category]
* [!UICONTROL Most Viewed by Item Attribute]
* [!UICONTROL Top Sellers Across the Site]
* [!UICONTROL Top Sellers by Category]
* [!UICONTROL Top Sellers by Item Attribute]
* [!UICONTROL Top by Analytics Metric]

**Vereiste parameters voor entiteit**

* `entity.categoryId` of het kenmerk item voor populariteit als de criteria zijn gebaseerd op het huidige item of het kenmerk item.
* Er mag niets worden doorgegeven voor de meest bekeken/verkochte objecten op de site.

**Leesingen**

* [Gebaseerd op populariteit](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 1.9: Objectcriteria {#item}

Aanbevelingen doen op basis van het zoeken naar objecten die vergelijkbaar zijn met een item dat de gebruiker bekijkt of onlangs heeft bekeken.

+++Zie details

**Beschikbare criteria**

* [!UICONTROL People Who Viewed This, Viewed That]
* [!UICONTROL People Who Viewed This, Bought That]
* [!UICONTROL People Who Bought This, Bought That]
* [!UICONTROL Items with Similar Attributes]

**Vereiste parameters voor entiteit**

* `entity.id` of een profielkenmerk dat als sleutel wordt gebruikt

**Leesingen**

* [Object gebaseerd](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 1.10: Gebruikerscriteria {#user}

Aanbevelingen doen op basis van het gedrag van de gebruiker.

+++Zie details

**Beschikbare criteria**

* [!UICONTROL Recently Viewed Items]
* [!UICONTROL Recommended for You]

**Vereiste parameters voor entiteit**

* `entity.id`

**Leesingen**

* [Op gebruiker gebaseerd](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 1.11: Aangepaste criteria {#custom}

Aanbevelingen doen op basis van een aangepast bestand dat u uploadt.

+++Zie details

**Beschikbare criteria**

* [!UICONTROL Custom algorithm]

**Vereiste parameters voor entiteit**

`entity.id` of het kenmerk dat wordt gebruikt als een sleutel voor het aangepaste algoritme

**Leesingen**

* [Aangepaste criteria](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 1.12: Vermeld de kenmerken die in de opnemingsregels worden gebruikt {#inclusion}

+++Zie details

**Leesingen**

* [Regels voor dynamische en statische integratie gebruiken](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 1.13: Uitgesloten id&#39;s verstrekken {#exclude}

Geef entiteit-id&#39;s door voor entiteiten die u wilt uitsluiten van uw aanbevelingen. U kunt bijvoorbeeld items uitsluiten die zich al in het winkelwagentje bevinden.

+++Zie details

**Leesingen**

* [Kan ik een entiteit dynamisch uitsluiten?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 1.14: Geef de `entity.event.detailsOnly=true` parameter {#true}

Entiteitskenmerken gebruiken om product- of inhoudsinformatie door te geven aan [!DNL Target Recommendations].

+++Zie details

**Leesingen**

* [Entiteitskenmerken](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=en){target=_blank}

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 1.15: Externe gegevenstoewijzing configureren (extern)

Deze stap zorgt ervoor dat alle gegevens die moeten worden verzonden naar [!DNL Target] is ingesteld.

+++Zie details

![Extern gegevenstoewijzingsdiagram](/help/dev/patterns/recs-atjs/assets/remote-data-mapping-combined.png){width="400" zoomable="yes"}

**Vereisten**

* De laag van gegevens zou met alle gegevens klaar moeten zijn die moeten worden verzonden naar [!DNL Target].

**Gegevensproviders instellen**

Zie voor meer informatie [Gegevensleveranciers](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

**Leesingen**

[targetPageParams, functie](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Handelingen**

Gebruik de `targetPageParams()` functie om alle vereiste gegevens in te stellen waarnaar moet worden verzonden [!DNL Target].

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 1.16: Belasting bij.js {#web}

Deze stap zorgt ervoor dat de JavaScript-bibliotheek at.js wordt geladen en geïnitialiseerd.

+++Zie details

![Adobe Target laden bij.js-diagram](/help/dev/patterns/recs-atjs/assets/load-atjs-combined.png){width="400" zoomable="yes"}

**Vereisten**

* Download of vraag uw digitale marketingteam naar de `at.js 2.*x*` JavaScript-bibliotheekbestand.

*Leesingen*

* [Hoe Target werkt](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html){target=_blank}
* [Hoe werkt at.js](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
* [Doel implementeren zonder tagbeheer](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

**Handelingen**

Sluit het bestand at.js in op al uw webpagina&#39;s waar u moet experimenteren, optimaliseren, personaliseren en gegevens verzamelen.

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)





























