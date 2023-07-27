---
keywords: global mbox, standaard doel, algemene mbox van doel gebruiken
description: Leer hoe u een verouderde globale box voor uw [!DNL Adobe Target] activiteiten als u al een global mbox op uw pagina's hebt gemaakt voor uw oudere implementaties.
title: Kan ik een globale box van een Verouderde implementatie gebruiken?
feature: at.js
exl-id: fe608b5e-ff66-4ba2-a622-d4f7307a9ca9
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Een globale box uit een oudere implementatie gebruiken

Standaard, [!DNL Target] maakt een globale mbox met de naam target-global-mbox, die wordt gebruikt voor het uitvoeren van activiteiten die zijn gemaakt in [!DNL Target]. Als u echter al een algemeen mbox op uw pagina&#39;s hebt gemaakt voor uw oudere implementaties, kunt u dat mbox gebruiken voor uw [!DNL Target] activiteiten.

>[!NOTE]
>
>Per account kunt u slechts één globale box gebruiken.

Om uw bestaande globale mbox voor allebei te gebruiken [!DNL Target] en uw oudere implementatie, moet u een paar parameters plaatsen.

1. Ga naar [!DNL Target]en klik vervolgens op **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

   Standaard, **[!UICONTROL Page load enabled (Auto-create global mbox]** is ingeschakeld en krijgt de aangepaste algemene mbox een naam `target-global-mbox`.

1. Als u een bestaande mbox wilt gebruiken, maak onbruikbaar **[!UICONTROL Page load enabled (Auto-create global mbox]** en geeft u de naam op van een eerder gemaakt algemeen naamvak in het dialoogvenster **[!UICONTROL Global Mbox]** veld.

   In de vervolgkeuzelijst Global Mbox worden alle vakken in uw account weergegeven. Als u een mbox wilt gebruiken die nog niet bestaat, maakt u de mbox.

1. Klik op **[!UICONTROL Save]**.

   De instellingen voor uw account worden bijgewerkt.

1. Download het nieuwe bestand at.js en verwijs ernaar op uw site.

   Alle bestaande activiteiten worden bijgewerkt om de opgegeven global mbox te gebruiken, inclusief activiteiten die eerder zijn gemaakt en geïmplementeerd.

## Problemen met de globale mbox-implementatie oplossen

De volgende FAQs kan worden gebruikt om uw globale mbox implementatie problemen op te lossen:

### Waarom wordt het globale selectievakje niet geladen, of waarom is er latentie bij het laden van het globale selectievakje wanneer de pagina wordt geladen?

Zorg ervoor dat de verwijzing at.js de eerste JavaScript-aanroep op de pagina is. Voor andere oplossingen voor dit probleem raadpleegt u [Algemene mbox Veelgestelde vragen](/help/dev/implement/client-side/atjs/global-mbox/global-mbox-faq.md).
