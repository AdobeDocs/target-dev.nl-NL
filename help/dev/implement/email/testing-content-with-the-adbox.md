---
keywords: Implementatie, niet-javascript, mbox, adbox
description: Een AdBox gebruiken om afbeeldingen te leveren in een externe implementatie met behulp van [!DNL Adobe Target]. Een AdBox is vergelijkbaar met een box, maar wordt bestuurd door een URL in plaats van JavaScript.
title: Hoe maak ik een Adbox voor een afbeelding?
feature: Implement Email
exl-id: ad1eb6c4-7a16-4054-ae76-57971261e931
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Een dialoogvenster maken voor een afbeelding

Een AdBox gebruiken om afbeeldingen te leveren in een externe implementatie met behulp van [!DNL Adobe Target].

Een AdBox is vergelijkbaar met een box, maar wordt beheerd door een URL in plaats van JavaScript. AdBox wordt gemaakt met een speciale URL voor een advertentievak die een advertentievak (of advertentievak) in uw Adobe-account laadt. Gebruik deze AdBox in plaats van de box in uw activiteiten. Gebruik de URL van het AdBox in plaats van een verwijzing naar een directe afbeelding in e-mail of andere niet-JavaScript-implementaties.

Zie voor hulp bij het selecteren van de juiste instellingen [Implementaties die niet op JavaScript zijn gebaseerd](/help/dev/implement/email/overview.md).

1. Maak de URL van het advertentievak:

   ```
   https://myClientCode.tt.omtrdc.net/m2/myClientCode/ubox/
   image?mbox=emailHeroImage123_320x200&
   mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fimg%2Flogo%2Egif
   ```

   * Wanneer `myClientCode` is de clientcode van uw bedrijf. De clientcode van uw bedrijf is helemaal in kleine letters en heeft geen speciale tekens.

     Uw clientcode is beschikbaar boven aan het dialoogvenster **[!UICONTROL Administation]** > **[!UICONTROL Implementation]** pagina van de [!DNL Target] interface.

   * Wanneer `image` is het vraagtype. In dit geval is het een afbeelding.

   * Wanneer `emailHeroImage123_320x200` is de naam van de advertentievak.

   * Wanneer `http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fimg%2Flogo%2Egif` is de standaardinhoud van de box. Dit moet een afbeelding zijn.

     Dit moet URL gecodeerd zijn en moet een absolute verwijzing zijn. U kunt de [HTML URL-coderingsverwijzing](https://www.w3schools.com/tags/ref_urlencode.asp) om uw URL&#39;s snel te coderen.

1. Maken [Omleidingsvoorstellen](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=nl-NL) voor elke alternatieve afbeelding.

   >[!NOTE]
   >
   >AdBox moet met een omleidingsvoorstel worden geladen of de standaardinhoudsaanbieding. Andere aanbiedingstypen werken niet. Omdat AdBox een URL is, kan het slechts URLs tonen het ontvangt, zodat werkt slechts de OmleidingsAanbieding.

1. Maak de activiteit.

   Zie [Implementaties die niet op JavaScript zijn gebaseerd](/help/dev/implement/email/overview.md) voor de juiste opstelling om uw doelstellingen te ontmoeten.

1. Volledige kwaliteitscontrole op de activiteit.

   Als beste praktijken, creeer een dummypagina en verifieer dat alle ervaringen, standaardinhoud, en rapporten zoals verwacht op alle browser types, voor al uw milieu&#39;s handelen.

1. Start de activiteit.
