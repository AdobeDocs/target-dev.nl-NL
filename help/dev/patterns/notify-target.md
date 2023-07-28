---
title: Doel op hoogte stellen
description: Zorg ervoor dat alle gebeurtenissen die moeten worden bijgehouden door [!DNL Target] worden verzonden met de methode trackEvent.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 65cad3c558aa0f52c8007dcdb566c0ce3b29d8b7
workflow-type: tm+mt
source-wordcount: '337'
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

![Doeldiagram waarschuwen](/help/dev/patterns/assets/diagram-notify-target.png){width="600" zoomable="yes"}

## Vuur [!DNL Adobe Target] Track-API

Deze stap helpt u ervoor te zorgen dat alle gebeurtenissen waarnaar moet worden verzonden [!DNL Target] worden verzonden met de `trackEvent` methode.

+++Zie details

![Fire Adobe Target Track API-diagram](/help/dev/patterns/assets/fire-adobe-target-track-api-diagram.png){width="100" zoomable="yes"}

U verzendt de kenmerken voor orderomzetting zoals vermeld in de sectie Voorwaarde hieronder. De naam van de box is niet van belang, maar de conversie moet worden gebruikt `orderConfirmPage`.

U te hoeven niet om de attributen van de ordeconversie in deze vraag te omvatten. Deze vraag registreert ideaal succesmetriek die van als mini-omzettingsgebeurtenissen vóór de belangrijkste omzettingsgebeurtenissen kan worden gedacht. `CardIds` moeten worden opgenomen in aanbevelingen op basis van de `Add to Cart` gebeurtenis.

**Vereisten**

* Ontmoet met uw bedrijfsteam om alle gebeurtenissen te identificeren die als omzettings of succesmetriek kunnen worden beschouwd. U moet ook de omzettingsgebeurtenis identificeren die opbrengst produceert zodat die details kunnen worden verzonden naar [!DNL Target] samen met de gebeurtenisgegevens.
* Zorg ervoor dat de volgende kenmerken beschikbaar zijn in de gegevenslaag, zodat u deze kunt verzenden met de conversiegebeurtenis. De conversiegebeurtenis genereert inkomsten, zoals een productaankoop of de gebeurtenis Add to Cart.

   * `productPurchaseId`: Product-id&#39;s die zijn aangeschaft als onderdeel van de bestelling. Meerdere producten worden door komma&#39;s gescheiden.
   * `orderTotal`: Totaal bestellen voor de aankoop.
   * `orderId`: Order-id van de aankoop.

* Als u een gebeurtenis bijhoudt voor toevoegen aan winkelwagentje, verzendt u `cartIds` als parameter. Een door komma&#39;s gescheiden lijst met product-id&#39;s kan worden doorgegeven voor `cardIds`.

**Leesingen**

* [adobe.target.trackEvent(), methode](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
* [cartID&#39;s voor op karretjes gebaseerde criteria](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based){target=_blank}

**Handelingen**

* Gebruiken `adobe.target-trackEvent()` methode om alle gegevens te verzenden die moeten worden verzonden naar [!DNL Target].







