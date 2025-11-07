---
title: Adobe Analytics for Target (A4T) Aanmelden bij Experience Platform Web SDK
description: Leer hoe te om de inzameling van Adobe Analytics voor Doel (A4T) gegevens te controleren gebruikend het Web SDK van Experience Platform.
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;logging;analytics;sdk;web sdk;
feature: Implementation
exl-id: 886588bf-4416-4f1e-aecc-467e48c8fb23
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# [!DNL Adobe Analytics for Target] (A4T) aanmelden bij [!DNL Experience Platform Web SDK]

Wanneer u [!DNL Adobe Target] gebruikt voor personalisatie, kunt u kiezen welk systeem u wilt gebruiken voor prestatiemeting. Elk [ activiteit van het Doel ](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) staat u toe om tussen [!DNL Target] het melden en Adobe [!DNL Analytics] het melden te selecteren.

Als u [!DNL Analytics] reporting gebruikt, moet [!DNL Target] het volgende meedelen aan [!DNL Analytics]:

* Welke [!DNL Target] activiteit uw bezoekers zijn ingegaan
* Welke ervaring ze hebben gezien
* Welke conversie is bereikt

De instructie [!DNL Adobe Experience Platform Web SDK] ondersteunt twee typen [!DNL Analytics] logging for [!UICONTROL Analytics for Target] (A4T) -gebruiksgevallen:

| Logmethode | Beschrijving |
| --- | --- |
| Logboekregistratie op de server [!DNL Analytics] | Alle [!DNL Analytics] -resultaten die via de Edge Network worden verzonden, worden vergroot met [!DNL Target] -gegevens aan de serverzijde, zonder dat u het detectieproces hoeft te doorlopen. |
| Logboekregistratie op de client [!DNL Analytics] | [!DNL Target] gegevens zijn teruggekeerd op de cliëntkant, toestaand u om gegevens aan [!DNL Analytics] manueel te verhogen en te verzenden gebruikend de [ Invoeging API van Gegevens ](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

De registrerenmethode wordt bepaald door of u [!DNL Adobe Analytics] toegelaten op uw gevormde [ datastream ](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) hebt:

![ Logging van de methodebeslissingsstroom ](/help/dev/implement/a4t/assets/analytics-logging.png)

## Volgende stappen

Dit document verstrekte een korte inleiding aan de verschillende registrerenmethodes voor gegevens A4T in het Web SDK. Raadpleeg de volgende documentatie voor meer informatie over elk van deze methoden:

* [Logboekregistratie op de server voor A4T-gegevens in Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)
* [Logboekregistratie op de client voor A4T-gegevens in de Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)
