---
title: Renderervaringen
description: Zorg ervoor dat alle noodzakelijke stappen voor renderervaringen in de juiste volgorde worden uitgevoerd.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 9b65380febf64896a3885c49f8bb79e4bb33f604
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# Renderervaringen

Voer de stappen in het dialoogvenster *Ervaringen renderen* diagram om ervoor te zorgen dat alle noodzakelijke taken nodig om ervaringen terug te geven in de correcte opeenvolging worden uitgevoerd.

>[!TIP]
>
>Klik op de afbeeldingen in dit onderwerp om het scherm in te vouwen.

## Renderervaringsdiagram {#diagram}

De automatische uit-van-de-doos flikkerbehandeling beschikbaar met at.js is zinvol slechts wanneer u hebt [!UICONTROL Automatic Page Load Request] ingeschakeld. Met deze optie verbergt u het hele lichaam van de HTML en haalt u de ervaringen op van [!DNL Target]. In dit geval is het uw verantwoordelijkheid om flikkering te behandelen. Zoek naar implementatiepatronen beschikbaar voor flikkering behandeling voor begeleiding.

De stapnummers in de volgende afbeelding komen overeen met de onderstaande secties.

![Renderervaringsdiagram](/help/dev/patterns/assets/diagram-render-experiences.png){width="600" zoomable="yes"}

Klik op de volgende koppelingen om naar de gewenste secties te navigeren:

* [3.1. Promotie](#promotion)
* [3.2: op auto&#39;s gebaseerde criteria](#cart)
* [3.3: criteria op basis van populariteit](#popularity)
* [3.4: Itemcriteria](#item)
* [3.5: Gebruikerscriteria](#user)
* [3.6: Aangepaste criteria](#custom)
* [3.7. Kenmerken verstrekken die in de opnemingsregels worden gebruikt](#inclusion)
* [3.8: Uitgesloten id&#39;s verstrekken](#exclude)
* [3.9: Geef entiteitskenmerken op om de productcatalogus voor Recommendations bij te werken](#entity-attributes)
* [3.10: Profielkenmerken opgeven die worden gebruikt als sleutels voor regels voor opname](#keys)
* [3.11: Aanvraag voor het laden van een brandpagina](#fire)
* [3.12: Aanvraag voor regionale locatie voor brand](#location)

## 3.1. Promotie {#promotion}

Aanbevolen objecten toevoegen en de plaatsing ervan in de doelRecommendations controleren [ontwerpen](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++Zie details

**Beschikbare opties**

* Promoten met id&#39;s
* [Bevorderen per collectie](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Promoten op kenmerk](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Vereiste parameters voor entiteit**

* Het kenmerk Item in promoties moet worden doorgegeven wanneer de optie &#39;Promoten door kenmerk&#39; wordt gebruikt.

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 3.2: op auto&#39;s gebaseerde criteria {#cart}

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

## 3.3: criteria op basis van populariteit {#popularity}

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

* `entity.categoryId` of het itemkenmerk voor populariteit als de criteria zijn gebaseerd op het huidige of het itemkenmerk.
* Er mag niets worden doorgegeven voor de meest bekeken/verkochte objecten op de site.

**Leesingen**

* [Gebaseerd op populariteit](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 3.4: Itemcriteria {#item}

Aanbevelingen doen op basis van het zoeken naar objecten die vergelijkbaar zijn met een item dat de gebruiker bekijkt of onlangs heeft bekeken.

+++Zie details

**Beschikbare criteria**

* [!UICONTROL People Who Viewed This, Viewed That]
* [!UICONTROL People Who Viewed This, Bought That]
* [!UICONTROL People Who Bought This, Bought That]
* [!UICONTROL Items with Similar Attributes]

**Vereiste parameters voor entiteit**

* `entity.id`
* Als een profielkenmerk wordt gebruikt als een sleutel

**Leesingen**

* [Object gebaseerd](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 3.5: Gebruikerscriteria {#user}

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

## 3.6: Aangepaste criteria {#custom}

Aanbevelingen doen op basis van een aangepast bestand dat u uploadt

+++Zie details

**Beschikbare criteria**

* [!UICONTROL Custom algorithm]

**Vereiste parameters voor entiteit**

`entity.id` of het kenmerk dat wordt gebruikt als een sleutel voor het aangepaste algoritme

**Leesingen**

* [Aangepaste criteria](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 3.7. Kenmerken verstrekken die in de opnemingsregels worden gebruikt {#inclusion}

+++Zie details

**Leesingen**

* [Regels voor dynamische en statische integratie gebruiken](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 3.8: Uitgesloten id&#39;s verstrekken {#exclude}

Geef entiteit-id&#39;s door voor entiteiten die u wilt uitsluiten van uw aanbevelingen. U kunt bijvoorbeeld items uitsluiten die zich al in het winkelwagentje bevinden.

+++Zie details

**Leesingen**

* [Kan ik een entiteit dynamisch uitsluiten?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 3.9: Geef entiteitskenmerken op om de productcatalogus voor [!DNL Recommendations] {#entity-attributes}

+++Zie details

**Leesingen**

* [Entiteitskenmerken](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

U kunt deze stap ook uitvoeren door productfeeds te maken met de opdracht [!DNL Target] UI voor het bijwerken van de productcatalogus voor [!DNL Recommendations].

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 3.10: Profielkenmerken opgeven die worden gebruikt als sleutels voor regels voor opname {#keys}

Geef de profielkenmerken op die als sleutels voor inclusieregels in de hierboven vermelde criteria van Recommendations worden gebruikt.

+++ Zie details

**Leesingen**

* [Profielkenmerken](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html){target=_blank}

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 3.11: Aanvraag voor het laden van een brandpagina {#fire}

Deze stap activeert een [!DNL Delivery API] bellen met `execute` > `pageLoad` lading in het verzoek. De `getOffers()` de methode haalt de ervaring en `applyOffers()` geeft de ervaring op de pagina weer. De pageLoad-aanvraag is nodig voor rendering van ervaringen die zijn geschreven in het dialoogvenster [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank} (VEC).

+++Zie details

![Vuur paginaoplaadaanvraagdiagram](/help/dev/patterns/assets/fire-page-load-request.png){width="100" zoomable="yes"}

**Vereisten**

* Alle gegevens moeten worden toegewezen met behulp van de `targetPageParams` functie.

**Leesingen**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Handelingen**

* Gebruik de `getOffers` en `applyOffers` methoden om de ervaring op te halen met een API-aanroep voor laden van pagina.

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 3.12: Aanvraag voor regionale brandlocatie (#location)

Deze stap activeert een [!DNL Delivery API] bellen met `execute` > `mboxes` lading in zijn verzoek. De `getOffers` de methode haalt de ervaring en `applyOffers` geeft de ervaring aan de pagina terug. U kunt meer dan één box onder `execute` > `mboxes` lading.

+++Zie details

![Aanvraagdiagram voor regionale locatie](/help/dev/patterns/assets/fire-regional-location-request.png){width="100" zoomable="yes"}

**Vereisten**

* Alle gegevens moeten worden toegewezen met behulp van de `targetPageParams` functie.

**Leesingen**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Handelingen**

* Gebruik de `getOffers` en `applyOffers` methoden om de ervaring op te halen met een API-aanroep voor laden van pagina.

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)