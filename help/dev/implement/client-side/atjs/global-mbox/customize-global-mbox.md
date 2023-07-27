---
keywords: global mbox, aanpassen global mbox, bewerken at.js, at.js, implementeren at.js
description: Leer hoe u een algemene mbox voor at.js kunt aanpassen op het tabblad [!UICONTROL Administration]-[!UICONTROL Implementation] pagina in [!DNL Adobe Target].
title: Hoe kan ik een globale box aanpassen?
feature: at.js
exl-id: f7809c3d-6e77-4bbe-8da3-4ab0a448c801
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Een globale box aanpassen

Informatie die u helpt bij het aanpassen van [!DNL Adobe Target] global mbox for at.js.

1. Klik op **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

1. Uitschakelen **[!UICONTROL Page load enabled (Auto create global mbox)]** Voeg vervolgens de naam toe van het aangepaste globale selectievakje dat u wilt gebruiken om activiteiten te leveren van [!DNL Target].

>[!WARNING]
>
>De wijziging wordt automatisch opgeslagen wanneer u een ander algemeen vakje selecteert.

Dit aangepaste globale vakje wordt ook gebruikt voor klik het volgen.

![custom-global-mbox](../../assets/custom-global-mbox.png)

1. Implementeer de bibliotheek at.js op uw site.

   Zie [Hoe te opstellen bij.js](/help/dev/implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md) voor meer informatie .

1. Tijd de overgang met uw versie.

   Wanneer u klaar bent voor [!DNL Target] om uw globale mbox voor alle activiteiten in de toekomst te beginnen gebruiken, kunt u met deze stap te werk gaan.

   Werk de naam van de aangepaste globale box bij zodat deze overeenkomt met de naam die in Stap 2, hierboven, wordt gebruikt.


>[!WARNING]
>
>Alle activiteiten in uw account worden gesynchroniseerd met dit selectievakje. Zorg ervoor dat de globale box op uw plaats aanwezig is zodat de activiteiten blijven functioneren. Zorg ervoor dat u de desbetreffende activiteiten die zijn gemaakt met de [!UICONTROL Visual Experience Composer] (VEC) die synchroniseren met deze box. Het is niet nodig om de in de [!UICONTROL Form-Based Experience Composer] of via API.
