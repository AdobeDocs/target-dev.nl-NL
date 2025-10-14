---
title: Logboekregistratie op de server voor A4T-gegevens in Experience Platform Web SDK
description: Leer hoe te om server-zijregistreren voor Adobe Analytics voor Doel (A4T) toe te laten gebruikend het Web SDK van Experience Platform.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;platform;logging;
feature: Implementation
source-git-commit: b1b0424bfe61fb8b4e88723e6bb2c565d75f8351
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Logboekregistratie op de server voor A4T-gegevens in [!DNL Experience Platform Web SDK]

Met [!DNL Adobe Experience Platform Web SDK] kunt u de functionaliteit [!UICONTROL Adobe Analytics for Target] (A4T) implementeren op [!UICONTROL Experience Platform Edge Network] . Wanneer logboekregistratie aan de serverzijde is ingeschakeld, worden alle [!DNL Analytics] -resultaten die via de Edge Network worden verzonden, aangevuld met [!DNL Target] -gegevens aan de serverzijde, zonder dat het aanraakproces hoeft te worden doorlopen.

Logboekregistratie op de server voor [!DNL Analytics] wordt ingeschakeld wanneer [!DNL Analytics] is ingeschakeld in de configuratie van de gegevensstroom:

![&#x200B; toegelaten de gegevensstroomconfiguratie van Analytics &#x200B;](/help/dev/implement/a4t/assets/enable-analytics-datastream.png)

In het volgende diagram ziet u hoe gegevens door het systeem stromen wanneer het aanmelden via de server is ingeschakeld: [!DNL Analytics]

![&#x200B; server-kant registrerenstroom &#x200B;](/help/dev/implement/a4t/assets/analytics-server-side-logging.png)

## Volgende stappen

Deze gids behandelde server-zijregistreren voor A4T gegevens in het Web SDK. Zie de gids op [&#x200B; cliënt-kant registreren &#x200B;](/help/dev/implement/a4t/client-side-logging.md) voor meer informatie over hoe te om A4T gegevens op de cliëntkant te behandelen.