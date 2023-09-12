---
title: Gegevensverzameling configureren
description: Zorg ervoor dat alle noodzakelijke taken voor gegevensverzameling in de juiste volgorde worden uitgevoerd.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 6cd78f8e3cbdd97a09b0cb6ca3af55994e85f819
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Gegevensverzameling configureren

Voer de stappen in het dialoogvenster *Gegevensverzameling* diagram om ervoor te zorgen dat alle noodzakelijke taken nodig voor gegevensinzameling in de correcte opeenvolging worden uitgevoerd.

>[!TIP]
>
>Klik op de afbeeldingen in dit onderwerp om het scherm in te vouwen.

De gegevenslaag is gereed tijdens het laden van de pagina of de gegevenslaag wordt gewijzigd nadat de pagina is geladen.

Als u al gegevens hebt toegewezen tijdens het [SDK-fase initialiseren](/help/dev/patterns/recs-atjs/initialize-sdk.md), moet u de stappen in dit diagram uitvoeren als:

* De gegevenslaag wordt op elke manier op dezelfde pagina uitgebreid en u wilt die aanvullende gegevens naar [!DNL Target]
* U wilt productcatalogusgegevens verzenden naar [!DNL Target Recommendations]

## Gegevensdiagram verzamelen {#diagram}

De stapnummers in de volgende afbeelding komen overeen met de onderstaande secties.

![Gegevensverzamelingsdiagram](/help/dev/patterns/recs-atjs/assets/data-collection-diagram.png){width="600" zoomable="yes"}

Klik op de volgende koppelingen om naar de gewenste secties te navigeren:

* [2.1: Gegevenstoewijzing configureren](#configure)
* [2.2 Koppeling naar entiteitskenmerken](#entity-attributes)
* [2.3 Druk de Adobe Target Track API in brand](#fire-api)

## 2.1: Gegevenstoewijzing configureren {#configure}

Deze stap helpt ervoor te zorgen dat alle gegevens die moeten worden verzonden naar [!DNL Adobe Target] is ingesteld.

+++Zie details

![Gegevenstoewijzingsdiagram configureren](/help/dev/patterns/recs-atjs/assets/cofigure-data-mapping.png){width="400" zoomable="yes"}

**Vereisten**

* De laag van gegevens zou met alle gegevens klaar moeten zijn die moeten worden verzonden naar [!DNL Target].

**Leesingen**

[targetPageParams, functie](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Handelingen**

Gebruik de `targetPageParams()` functie om alle vereiste gegevens in te stellen waarnaar moet worden verzonden [!DNL Target].

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 2.2: Koppeling naar entiteitskenmerken {#entity-attributes}

Koppeling naar entiteitskenmerken om de productcatalogus bij te werken voor [!DNL Target Recommendations].

+++Zie details

**Leesingen**

* [Entiteitskenmerken](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Overwegingen**

* Een andere manier om entiteitattributen door te geven is de productcatalogus in bij te werken [!DNL Target] Gebruikersinterface [Recommendations-productfeeds](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank}.
* Het overgaan van entiteitattributen is van toepassing slechts op pagina&#39;s waar product-catalogus gegevens op de gegevenslaag beschikbaar zijn.
* Het overgaan van `entity.event.detailsOnly=true` parameter in om het even welke vraag neemt prioriteit.

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

## 2.3 Druk de Adobe Target Track API in brand {#fire-api}

Deze stap helpt ervoor te zorgen dat alle gegevens die moeten worden verzonden naar [!DNL Target] wordt verzonden.

+++Zie details

![Fire Adobe Target Track API-diagram](/help/dev/patterns/recs-atjs/assets/fire-track-api.png){width="400" zoomable="yes"}

**Vereisten**

* Alle gegevenstoewijzingen moeten zijn uitgevoerd met behulp van de [targetPageParams, functie](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Leesingen**

* [adobe.target.trackEvent(), methode](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)

**Handelingen**

Gebruiken [adobe.target.trackEvent(), methode](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) om alle gegevens te verzenden die moeten worden verzonden naar [!DNL Target].

+++

[Keer aan het diagram bij de bovenkant van deze pagina terug.](#diagram)

