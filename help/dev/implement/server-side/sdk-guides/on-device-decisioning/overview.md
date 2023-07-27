---
keywords: serverzijde, serverzijde, sdk, sdks, op apparaat, besluit, op apparaat, op apparaat, nul latentie, latentie, bijna nul, node.js, serverzijde3
description: Leren gebruiken [!UICONTROL [!UICONTROL on-device decisioning]] om uw [!DNL Target] A/B en MVT activiteiten op uw server om in-geheugenbesluit bij bijna-nul latentie uit te voeren.
title: Wat is een apparaatbeslissing?
feature: Implement Server-side
exl-id: 22ed3072-56f0-4075-9d1a-d642afe3b649
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 0%

---

# Overzicht van apparaatbeslissingen

De volgende generatie [!DNL Adobe Target] SDK&#39;s bieden nu [!UICONTROL on-device decisioning], die de capaciteit verstrekt om uw A/B en Ervaring het richten (XT) campagnes op uw server in het voorgeheugen op te slaan en in geheugenbesluit bij bijna nul latentie uit te voeren, zonder netwerkverzoeken te blokkeren om [!DNL Adobe Target]&#39;s Edge Network.

[!DNL Adobe Target] Biedt ook de flexibiliteit om de meest relevante en bijgewerkte ervaring van uw experimenteren en ML-gedreven verpersoonlijkingscampagnes via een levende servervraag te leveren. Met andere woorden, wanneer prestaties het belangrijkst zijn, kunt u ervoor kiezen om [!UICONTROL on-device decisioning], maar wanneer de meest relevante en meest actuele ervaring nodig is, kan een servervraag in plaats daarvan worden gemaakt. Zie [wanneer moet u op het apparaat versus randbesluitvorming gebruiken](../../sdk-guides/on-device-decisioning/supported-features.md) voor meer informatie over gebruiksgevallen die het gebruik van een van beide rechtvaardigen.

>[!NOTE]
>
>Beslissing op het apparaat is beschikbaar voor zowel client-side als server-side implementaties. Dit artikel beschrijft [!UICONTROL on-device decisioning] voor server-kant. Voor informatie over [!UICONTROL on-device decisioning] voor client-side, raadpleeg de implementatiedocumentatie van de client-side [hier](../../../client-side/atjs/on-device-decisioning/on-device-decisioning.md).

## Hoe werkt het?

Wanneer u een [!DNL Adobe Target] SDK met [!UICONTROL on-device decisioning] enabled, a *regelartefact* wordt lokaal op uw server gedownload en in cache geplaatst, vanaf de Akamai CDN die het dichtst bij uw server ligt. Wanneer een verzoek om een [!DNL Adobe Target] De ervaring wordt gemaakt binnen uw server-zijtoepassing, het besluit betreffende welke inhoud om in geheugen terug te keren wordt gemaakt, die op de meta-gegevens wordt gebaseerd die in het caching regelartefact worden gecodeerd, dat al uw [!UICONTROL on-device decisioning] A/B en XT.

Het volgende diagram toont het [!UICONTROL on-device decisioning] architectuur. Klik om de afbeelding uit te vouwen.

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![Apparaatdiagram voor beslissingsarchitectuur](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/assets/asset-sdk-local-decisioning-architecture-diagram.png "Apparaatdiagram voor beslissingsarchitectuur"){zoomable=&quot;yes&quot;}

## Wat zijn de voordelen?

* **Lever bijna-nul latentiebesluiten.** De sluiting en de beslissing worden uitgevoerd in geheugen en op apparaat vermijden blokkerend netwerkverzoeken.
* **Verbeter de prestaties van de toepassing.** Voer experimenten uit en verpersoonlijking aan uw klanten en gebruikers zonder de ervaringen van de eindgebruiker in gevaar te brengen.
* **Kwaliteitsscore voor Google-site verbeteren.** Nu de beslissing in het geheugen en op de server plaatsvindt, verbetert u de score voor kwaliteit van de Google-site van uw online bedrijf om deze beter te kunnen ontdekken door de consument.
* **Leer van analyses in real time.** Krijg inzicht van uw prestaties van activiteit in real time via [!DNL Adobe Target] of A4T rapportering, toelatend u om uw strategie op kritieke momenten te draaien.

## Ondersteunde functionaliteit

### Activiteiten

Apparaatbeslissingen ondersteunen de volgende activiteitstypen die door de [Form-based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html):

* [!UICONTROL A/B Test]
* [!UICONTROL Experience Targeting] (XT)

### Toewijzingsmethode

Apparaatbeslissingen ondersteunen de volgende toewijzingsmethode:

* Handmatig

### Doelgerichtheid publiek

De besluitvorming op het apparaat ondersteunt de volgende publieksregels:

| Auditieregel | Apparaatbeslissingen |
| --- | --- |
| [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Ja |
| [Netwerk](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | Nee |
| [Mobiel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | Nee |
| [Aangepaste parameters](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Ja |
| [Besturingssysteem](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Ja |
| [Sitepagina&#39;s](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Ja |
| [Browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Ja |
| [Bezoekerprofiel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | Nee |
| [verkeersbronnen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | Nee |
| [Tijdschema](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Ja |
| [Experience Cloud publiek](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Soorten publiek uit Adobe Audience Manager, Adobe Analytics en Adobe Experience Manager) | Nee |

## Hoe kan ik mijn klant voorzien van [!UICONTROL on-device decisioning]?

Beslissing op het apparaat is beschikbaar voor iedereen [!DNL Adobe Target] klanten die [!DNL Adobe Target] SDK&#39;s aan serverzijde. Navigeer naar om deze functie in te schakelen **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** in de [!DNL Adobe Target] UI, en laat toe **[!UICONTROL On-Device Decisioning]** schakelen.

>[!NOTE]
>
>U moet de beheerder of fiatteur hebben *gebruikersrol* om de [!UICONTROL On-Device Decisioning] schakelen.

![alternatieve afbeelding](assets/asset-odd-toggle.png)

Na het inschakelen van de beslissingsschakelaar op het apparaat, [!DNL Adobe Target] beginnen met genereren en verspreiden *regelartefacten* voor uw client.

>[!NOTE]
>
>Zorg ervoor dat u de schakeloptie inschakelt voordat u de [!DNL Adobe Target] SDK voor gebruik [!UICONTROL on-device decisioning]. De regelartefacten zullen eerst aan Akamai CDNs moeten produceren en verspreiden opdat [!UICONTROL on-device decisioning] om te werken.

### Alle bestaande opnemen [!UICONTROL on-device decisioning] gekwalificeerde activiteiten in de artistieke schakelfunctie

Deze schakelen **op** wanneer u al uw levens wilt [!DNL Target] activiteiten waarvoor [!UICONTROL on-device decisioning] automatisch in het artefact worden opgenomen.

Deze schakeloptie verlaten **uit** betekent dat u elke [!UICONTROL on-device decisioning] activiteiten om deze in het gegenereerde artefact op te nemen.

## Hoe weet ik dat een activiteit [!UICONTROL on-device decisioning] geschikt?

Nadat u een activiteit creeert, een etiket genoemd **[!UICONTROL Decisioning Method]**, zichtbaar op de pagina met activiteitendetails, geeft aan of de activiteit [!UICONTROL on-device decisioning] geschikt.

![alternatieve afbeelding](assets/asset-odd9.png)

U kunt ook alle activiteiten zien die [!UICONTROL on-device decisioning] geschikt voor **[!UICONTROL Activities]** pagina door de kolom toe te voegen **[!UICONTROL Decisioning Method]** aan de lijst van activiteiten.

![alternatieve afbeelding](assets/asset-odd7.png)

>[!NOTE]
>
>Na het maken en activeren van een activiteit die [!UICONTROL on-device decisioning] geschikt, kan het 5-10 minuten nemen alvorens het in het regelvervorming inbegrepen is die aan Akamai CDN PoPs wordt geproduceerd en verspreid.

## Wat is de samenvatting van de stappen die ik moet volgen om mijn [!UICONTROL on-device decisioning] activiteiten worden via [!DNL Adobe Target]SDK aan serverzijde?

1. Toegang krijgen tot de [!DNL Adobe Target] UI en navigeer naar **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** de **[!UICONTROL On-Device Decisioning]** schakelen.
1. De optie **[!UICONTROL Include all existing [!UICONTROL on-device decisioning] qualified activities in the artifact]** schakelen.
1. Een type activiteit maken en activeren dat wordt ondersteund door [!UICONTROL on-device decisioning]en controleert of de **[!UICONTROL Decisioning Method]** is **[!UICONTROL On-Device Decisioning]** voor die activiteit.
1. Installeer de [Node.js](../../node-js/overview.md) of [Java](../../java/overview.md) SDK met `decisioningMethod = on-device`.
1. Implementeren `getOffers()` of `getAttributes()` in uw code om een ervaring op apparaat terug te winnen.
1. Implementeer uw code.

Voor voorbeelden die aantonen hoe u met bovenstaande stappen 1-3 kunt beginnen, raadpleegt u de [Aan de slag](../getting-started/getting-started.md) sectie.


## Aanvullende bronnen

### Webinar: Personaliseer en test met nul latentie met op apparaat besluiten van [!DNL Adobe Target]

Meer dan ooit, worden de marketers, de producteigenaars en de ontwikkelaars belast met het optimaliseren van de algemene klantenervaring op plaatsen, in apps, en overal anders zij met hun klanten verbinden. Meerdere gereedschappen met gegevenssilo&#39;s en ingewikkelde implementaties zijn ontoereikend.

In dit geregistreerde webinar: [!DNL Adobe Target] productdeskundigen bespreken hoe u met behulp van beslissingen voor optimalisatie van kritieke ervaringen op apparaten, die lokaal kunnen worden uitgevoerd met bijna-nullatentie, deuren kunt openen voor spannende nieuwe gebruiksgevallen en de prestaties van de site voor uw klanten kunt verbeteren.

>[!VIDEO](https://video.tv.adobe.com/v/328148/?quality=12)


### Lesbestand: beslissingen op het apparaat

[!DNL Adobe Target] [!UICONTROL on-device decisioning] maakt levering van inhoud met een minimale latentie mogelijk.

Deze video van 7 minuten:

* Beschrijft [!UICONTROL on-device decisioning], met inbegrip van de wijze waarop deze vergelijking maakt met andere methoden [!DNL Target] uitvoering
* Toont aan hoe te om toe te laten [!UICONTROL on-device decisioning] in doel
* Hiermee wordt een op een formulier gebaseerde componentactiviteit onderzocht die is geconfigureerd met JSON-inhoud
* Hiermee wordt de voorbeeldcode van Node.JS SDK weergegeven met de sleutelconfiguratie die is vereist voor [!UICONTROL on-device decisioning]
* Toont resultaten in browser aan

>[!VIDEO](https://video.tv.adobe.com/v/329032/?quality=12)

Zie de [[!DNL Adobe Target] Tutorials](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html).

### Adobe Tech Blog - Deel 1: Uitvoeren [!DNL Adobe Target] NodeJS SDK voor experimenteren en personalisatie op Edge-platforms (Akamai Edge Workers)

[Klik hier om het blogbericht te openen](https://medium.com/adobetech/part-1-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-4d8660964ed9).

### Adobe Tech Blog - Deel 2: Run [!DNL Adobe Target] NodeJS SDK voor experimenteren en personalisatie op Edge-platforms (AWS Lambda@Edge)

[Klik hier om het blogbericht te openen](https://medium.com/adobetech/part-2-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-aws-4d6bdac24563).
