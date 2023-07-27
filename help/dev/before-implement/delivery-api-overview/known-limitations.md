---
title: Overwegingen met betrekking tot de Adobe Target Delivery API en bekende beperkingen
description: Met welke overwegingen en bekende beperkingen moet ik rekening houden bij het gebruik van de [!UICONTROL Adobe Target Delivery API]?
keywords: aflevering api
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Overwegingen en bekende beperkingen

* Er is geen verificatie voor [!DNL Target] Leverings-API&#39;s.
* Deze API verwerkt geen cookies of leidt geen aanroepen om.
* Ondersteuning voor [!UICONTROL Automated Personalization] (AP) en [!UICONTROL Recommendations] activiteiten: Deze API heeft twee modi voor het ophalen van inhoud: uitvoeren en prefetch. De voorkeursmodus kan alleen worden gebruikt voor [!UICONTROL AB Test] en [!UICONTROL Experience Targeting] (XT) activiteiten. Gebruik de prefetch-modus niet voor [!UICONTROL Automated Personalization] (AP), [!UICONTROL Auto-Allocate], [!UICONTROL Auto-Target], of [!UICONTROL Recommendations] typen activiteiten.
* Zowel HTTP/1.1- als HTTP/2-headernamen zijn niet hoofdlettergevoelig. HTTP/2 dwingt echter kleine-hoofdheadernamen af. Zie de klasse [Document Hypertext Transfer Protocol versie 2 (HTTP/2)](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Als u een eindpunt gebruikt dat bezoekers door onze nieuwe infrastructuur van de Balancer van de Lading leidt, worden hun verbindingen automatisch bevorderd aan HTTP/2. Dit verbeteringsproces zet verzoekkopballen in kleine letters om zodat zullen zij niet misvormd worden beschouwd.

  Deze kwestie kan een kwestie voor klanten potentieel zijn als hun bibliotheken opstelling zijn om geval-gevoelige (specifiek niet in kleine letters) verzoek/reactiekkopballen te zoeken.
