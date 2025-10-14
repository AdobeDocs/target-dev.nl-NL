---
title: Overwegingen met betrekking tot de Adobe Target Delivery API en bekende beperkingen
description: Met welke overwegingen en bekende beperkingen moet ik rekening houden wanneer u de [!UICONTROL Adobe Target Delivery API] gebruikt?
keywords: aflevering api
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: 94a4122244065384f487ca9a29dfa1b414168cb8
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Overwegingen en bekende beperkingen

De volgende informatie geeft een overzicht van overwegingen en bekende beperkingen bij het gebruik van [!DNL Adobe Target] [!DNL Delivery API] .

* Er is geen verificatie voor [!DNL Target] Delivery-API&#39;s.
* Deze API verwerkt geen cookies of leidt geen aanroepen om.
* Zowel HTTP/1.1- als HTTP/2-headernamen zijn niet hoofdlettergevoelig. HTTP/2 dwingt echter kleine-hoofdheadernamen af. Voor meer informatie, zie de [&#x200B; Versie 2 van het Protocol van de Overdracht van de Hypertext (HTTP/2) documentatie &#x200B;](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Als u een eindpunt gebruikt dat bezoekers door onze nieuwe infrastructuur van de Balancer van de Lading leidt, worden hun verbindingen automatisch bevorderd aan HTTP/2. Dit verbeteringsproces zet verzoekkopballen in kleine letters om zodat zullen zij niet misvormd worden beschouwd.

  Deze kwestie kan een kwestie voor klanten potentieel zijn als hun bibliotheken opstelling zijn om geval-gevoelige (specifiek niet in kleine letters) verzoek/reactiekkopballen te zoeken.
