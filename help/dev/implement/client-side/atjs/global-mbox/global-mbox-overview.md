---
keywords: global mbox, implementeren op.js
description: Meer informatie over de globale box vindt u in [!DNL Adobe Target], a name used to refer to the single server call made at the top of each web page in your [!DNL Target] uitvoering.
title: Wat is een globale box?
feature: at.js
exl-id: 572c1dc6-5cdd-427a-9458-e5ec49990cf8
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# De globale box begrijpen

Informatie over globale mbox, een naam die wordt gebruikt om naar de enige servervraag te verwijzen die bij de bovenkant van elke Web-pagina in uw [!DNL Adobe Target] uitvoering.

Standaard krijgt het algemene mbox de naam `target-global-mbox`. U kunt de naam van uw account desgewenst wijzigen.

Er zijn verschillende verschillen tussen een standaard mbox (non-global mbox) en de globale mbox, waaronder:

| Standaardbox | Globale mbox |
|--- |--- |
| Een standaardkader loopt gewoonlijk rond de inhoud door een `<DIV>` -tag. | Het algemene mbox is &quot;leeg&quot; en loopt niet rond inhoud. |
| Inhoud van slechts één activiteit kan in een normale doos worden geleverd. | Inhoud uit meerdere activiteiten kan in één reactie op een global box worden geleverd. |

Als er meerdere activiteiten worden geleverd via de globale box of via meerdere gewone boxes, is het doel [bepaalt de prioriteit](https://experienceleague.adobe.com/docs/target/using/activities/priority.html) waardoor de activiteit (of activiteiten) aan een webpagina wordt (worden) geleverd.

Er kunnen aanvullende gegevens op paginaniveau worden verzonden naar [!DNL Target] samen met de globale box door `[!UICONTROL targetPageParams]` functie. Dit is vergelijkbaar met de functionaliteit van de mbox-parameter. Zie voor meer informatie [Parameters doorgeven aan een globale box](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).
