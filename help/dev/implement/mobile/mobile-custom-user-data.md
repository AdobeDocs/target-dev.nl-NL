---
keywords: mobiele app, mobiele app om gegevens te verzenden, mobiele toepassing, aangepaste mobiele gebruikersgegevens, aangepaste mobiele toepassingsgegevens
description: Leer hoe u aanvullende informatie over de locatie of de gebruiker kunt verzenden naar [!DNL Adobe Target] als naam-waardeparen om u te helpen douanepubliek bouwen.
title: Hoe kan ik aangepaste gebruikersgegevens verzenden in een iOS-app?
feature: Implement Mobile
exl-id: 9cf8e8fd-1898-43b1-b339-d7a21cb35d57
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# iOS - aangepaste gebruikersgegevens verzenden

U kunt aanvullende informatie over de locatie of de gebruiker naar [!DNL Target] als naam-waardeparen.

>[!IMPORTANT]
>
>Steun voor de [!DNL Adobe Mobile] versie 4.*x* SDK&#39;s zijn geëindigd op 31 augustus 2021 en worden niet langer aanbevolen voor [!DNL Adobe Target] mobiele gebruikers.
>
>De [Adobe Experience Platform SDK voor mobiele apps](https://developer.adobe.com/client-sdks/documentation/){target=_blank} is de aanbevolen oplossing voor stroom [!DNL Adobe Experience Cloud] oplossingen en services in uw mobiele apps.

Deze informatie kan worden gebruikt om aangepaste soorten publiek (bijvoorbeeld gebruikers met een lengte van meer dan 25000 mijl) en rapportage te maken.

Er zijn twee typen parameters die u kunt verzenden met een [!DNL Target] oproep:

* **mbox-parameters**: Mbox-parameters zijn niet blijvend in sessies.
* **Profielparameters**: Profielparameters worden opgeslagen in de opslag van het bezoekersprofiel en zijn tijdens sessies blijvend. mbox-parameters blijven niet bestaan. Terwijl sommige toetsen zijn gereserveerd, kunnen zowel profiel- als mbox-parameters aangepaste sleutel-waardeparen zijn.

Hoewel er enkele gereserveerde toetsen zijn, kunnen zowel profiel- als mapoparameters aangepaste sleutel-waardeparen bevatten.

1. Woordenboek maken.

   Maak eerst een woordenboek met de waarden waarnaar u verzendt [!DNL Target]. Voor het gemak kunt u dit toevoegen in het `welcomeMessageCampaign` methode zodat moet u zich niet over werkingsgebied ongerust maken.

   Hier volgt een voorbeeldwoordenboek. U kunt deze plakken in `(void)welcomeMessageCampaign`. De waarden voor toetsen als `userLevel` en `userMiles` zijn hard-gecodeerd in dit voorbeeld. Over het algemeen geeft u de bijbehorende variabelen door.

   ```
   NSDictionary *targetParams = [[NSDictionary alloc] initWithObjectsAndKeys: 
                                 @"platinum",@"userLevel", 
                                 @26500,@"userMiles", 
                                 @"1067007",@"entity.id", 
                                 @"dealsapp.qa", @"host", 
                                 @"fashion",@"entity.categoryId", 
                                 @"millenial", @"profile.persona", 
                                 @"cohort_5", @"profile.cohort", 
                                 nil];
   ```

   * Toetsen met het voorvoegselprofiel (bijvoorbeeld `profile.persona`) worden opgeslagen in het gebruikersprofiel.

     Deze profielkenmerken kunnen op verschillende activiteiten en kanalen worden gebruikt.

   * Toetsen die geen voorvoegsel hebben (bijvoorbeeld `userMiles`) zijn mbox-parameters.

     Deze parameters zijn alleen beschikbaar tijdens de sessie.

   * Toetsen met het voorvoegsel (bijvoorbeeld `entity.category.id`) worden gebruikt voor productaanbevelingen.

1. Controleer de gegevens.
   1. In toepassing `didFinishLaunchingWithOptions`, verwijderen of toevoegen `[ADBMobile setDebugLogging:YES];`.

      Hiermee worden gedetailleerde foutopsporingslogbestanden afgedrukt.
   1. Maak de app.
   1. Verifieer dat de parameters in de doelvraag worden overgegaan.

      Zoek naar uw naam van de doelplaats in uw zuivert console. U zult een vraag zien aan `YOUR-CLIENT-CODE.tt.omtrdc.net`met alle parameters die u net hebt doorgegeven.

      (Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

      ![Doellocatie in de foutopsporingsconsole](/help/dev/implement/mobile/assets/mobile-debug.png "Doellocatie in de foutopsporingsconsole"){zoomable="yes"}

   U kunt een publiek maken en de weergave van inhoud beperken of instellen met behulp van deze parameters in [!DNL Target].
