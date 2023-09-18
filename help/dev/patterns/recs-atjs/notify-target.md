---
title: Doel op hoogte stellen
description: Zorg ervoor dat alle gebeurtenissen die moeten worden bijgehouden door [!DNL Target] worden verzonden met de methode trackEvent.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 013a49b92357cfb5d45f7e595b46b1b12ce91c65
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Waarschuwen [!DNL Target]

Als u deze stap uitvoert, zorgt u ervoor dat alle gebeurtenissen waarnaar moet worden verzonden [!DNL Adobe Target] worden verzonden met de `trackEvent` methode.

Elke gebeurtenis die moet worden bijgehouden [!DNL Target] kan een primaire omzettingsgebeurtenis of een succesmetrisch zijn.

>[!TIP]
>
>Klik op de afbeeldingen in dit onderwerp om het scherm in te vouwen.

## Waarschuwen [!DNL Target] diagram {#diagram}

Het nummer van de stap in de volgende afbeelding komt overeen met de onderstaande sectie.

![Doeldiagram waarschuwen](/help/dev/patterns/recs-atjs/assets/diagram-notify-target.png){width="600" zoomable="yes"}

## 4.1. Vuur [!DNL Adobe Target] Track-API

Deze stap helpt u ervoor te zorgen dat alle gebeurtenissen waarnaar moet worden verzonden [!DNL Target] worden verzonden met de `trackEvent` methode.

+++Zie details

![Fire Adobe Target Track API-diagram](/help/dev/patterns/recs-atjs/assets/fire-adobe-target-track-api-diagram-combined.png){width="400" zoomable="yes"}

U verzendt de kenmerken voor orderomzetting die worden vermeld in het dialoogvenster *Vereisten* hieronder. De naam van de box is niet van belang, maar de conversie moet worden gebruikt `orderConfirmPage`.

U te hoeven niet om de attributen van de ordeconversie in deze vraag te omvatten. Deze vraag registreert ideaal succesmetriek die van als mini-omzettingsgebeurtenissen vóór de belangrijkste omzettingsgebeurtenissen kan worden gedacht. `CardIds` moeten worden opgenomen in aanbevelingen op basis van de `Add to Cart` gebeurtenis.

**Vereisten**

* Ontmoet met uw bedrijfsteam om alle gebeurtenissen te identificeren die als omzettings of succesmetriek kunnen worden beschouwd. U moet ook de omzettingsgebeurtenis identificeren die opbrengst produceert zodat die details kunnen worden verzonden naar [!DNL Target] samen met de gebeurtenisgegevens.
* Zorg ervoor dat de volgende kenmerken beschikbaar zijn in de gegevenslaag, zodat u deze kunt verzenden met de conversiegebeurtenis. De conversiegebeurtenis genereert inkomsten, zoals een productaankoop of de gebeurtenis Add to Cart.

   * `productPurchaseId`: Product-id&#39;s die zijn aangeschaft als onderdeel van de bestelling. Scheid meerdere producten met komma&#39;s.
   * `orderTotal`: Totaal bestellen voor de aankoop.
   * `orderId`: Order-id van de aankoop.

* Als u een gebeurtenis bijhoudt voor toevoegen aan winkelwagentje, verzendt u `cartIds` als parameter. Een door komma&#39;s gescheiden lijst met product-id&#39;s kan worden doorgegeven voor `cardIds`.

**Leesingen**

* [adobe.target.trackEvent(), methode](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
* [cartID&#39;s voor op karretjes gebaseerde criteria](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based){target=_blank}

**Handelingen**

* Gebruiken `adobe.target-trackEvent()` methode om alle gegevens te verzenden die moeten worden verzonden naar [!DNL Target].







