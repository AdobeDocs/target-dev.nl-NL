---
keywords: problemen oplossen, veelgestelde vragen, veelgestelde vragen, veelgestelde vragen, algemene en globale vragen
description: Lees veelgestelde vragen (FAQs) en antwoorden over Adobe [!DNL Target] globale vakken.
title: Wat worden vaak gestelde vragen over Global mbox?
feature: at.js
exl-id: 7bcd1b67-809a-466a-b648-6e0e44386157
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# Algemene mbox Veelgestelde vragen

Lijst met veelgestelde vragen (FAQ&#39;s) over globale vakken.

## Kan ik meer dan één globale box hebben als mijn [!DNL Target] account is ingesteld op meerdere domeinen?

Er wordt slechts één globale box ondersteund voor uw account.

U kunt beperken waar uw activiteiten lopen door URL-regels aan uw activiteiten toe te voegen. Zie voor meer informatie [Dezelfde ervaring opnemen op vergelijkbare pagina&#39;s](https://experienceleague.adobe.com/docs/target/using/experiences/vec/temtest.html).

U kunt ook een parameter op de pagina doorgeven met [targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) en selecteer vervolgens de parameters in de sectie &quot;URL configureren&quot; in het dialoogvenster [!UICONTROL Visual Experience Composer] (VEC) of door de parameters toe te voegen als &quot;verfijningen&quot; in de [!UICONTROL Form-Based Experience Composer].

## Hoe kan ik inkomstengegevens doorgeven aan een [!DNL Target] globale mbox?

Om opbrengst en ordeinformatie over target-global-mbox te verzamelen, moeten de &quot;mbox parameters&quot;worden verzonden naar [!DNL Target]. Deze parameters zijn naam/waardeparen die worden gebruikt om meer informatie naar te verzenden [!DNL Target]. [!DNL Target] zoekt automatisch naar deze parameters (gereserveerde namen) om inkomstengegevens te vullen.

Voor de `orderConfirmPage`, moet u `orderTotal`, `orderId`, en `productPurchasedId`.

Deze parameters moeten via `targetPageParams()`. Zie voor meer informatie [Parameters doorgeven aan een globale box](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).

U zult ook het richten aan het omzettingsstuk willen toevoegen zodat [!DNL Target] telt slechts omzettingen op doel-globaal-mbox wanneer de pagina van de ordesbevestiging is bekeken, zoals hieronder getoond:

![alternatieve afbeelding](assets/revenue1.png)

De sectie Site-pagina&#39;s die hierboven is weergegeven, bevat de volgende selecties: Huidige pagina, URL, bevat, ordende bevestiging.

![alternatieve afbeelding](assets/revenue2.png)

De opties in de bovenstaande afbeelding zijn onder andere:

* **Wat wilt u meten met deze activiteit?** Ontvangsten
* **Standaardweergave voor rapportage:** Opbrengst per bezoeker (RPV)
* **Welke actie heeft uw publiek ondernomen om aan te geven dat uw doel is bereikt?** Een mbox, target-global-mbox weergegeven
