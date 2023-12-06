---
title: Overwegingen met betrekking tot de Adobe Target Delivery API en bekende beperkingen
description: Met welke overwegingen en bekende beperkingen moet ik rekening houden bij het gebruik van de [!UICONTROL Adobe Target Delivery API]?
keywords: aflevering api
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: 49acf92bbe06dbcee36fef2b7394acd7ce37baad
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# Overwegingen en bekende beperkingen

* Er is geen verificatie voor [!DNL Target] Leverings-API&#39;s.
* Deze API verwerkt geen cookies of leidt geen aanroepen om.
* Zowel HTTP/1.1- als HTTP/2-headernamen zijn niet hoofdlettergevoelig. HTTP/2 dwingt echter kleine-hoofdheadernamen af. Zie de klasse [Document Hypertext Transfer Protocol versie 2 (HTTP/2)](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Als u een eindpunt gebruikt dat bezoekers door onze nieuwe infrastructuur van de Balancer van de Lading leidt, worden hun verbindingen automatisch bevorderd aan HTTP/2. Dit verbeteringsproces zet verzoekkopballen in kleine letters om zodat zullen zij niet misvormd worden beschouwd.

  Deze kwestie kan een kwestie voor klanten potentieel zijn als hun bibliotheken opstelling zijn om geval-gevoelige (specifiek niet in kleine letters) verzoek/reactiekkopballen te zoeken.
