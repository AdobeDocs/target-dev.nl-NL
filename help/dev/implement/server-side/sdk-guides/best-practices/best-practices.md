---
title: Tips en trucs bij het gebruik van apparaatbeslissingen
description: Tips en trucs leren tijdens het gebruik [!UICONTROL on-device decisioning] in [!DNL Adobe Target]
feature: Implement Server-side
exl-id: a0ca014d-ad9f-4ecc-961d-cb7ba236507f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Aanbevolen procedures

[!DNL Adobe] raadt de volgende aanbevolen procedures aan bij het gebruik van [!UICONTROL on-device decisioning]:

## Tips en trucs wanneer de beslissingsmethode &quot;op apparaat&quot; is

Wanneer u &quot;op het apparaat&quot; gebruikt als beslissingsmethode, wordt het artefact gedownload wanneer de bezoeker de webpagina voor het eerst laadt. Om het even welke activiteitenkwalificatie die op de eerste paginading (geen geheim voorgeheugen) moet gebeuren gebeurt slechts nadat het artefact volledig wordt gedownload. Er zijn bepaalde beste praktijken u kunt volgen om ervoor te zorgen dat de activiteitenkwalificaties voor een nieuwe anonieme bezoeker snel gebeuren.

* Deactiveer &quot;Op apparaat&quot;geschikt activiteiten die niet in het artefact bedoeld zijn.
* Als u Target Premium hebt, kunt u [eigenschappen/werkruimten](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=nl-NL) om verschillende artefactenbestanden te maken voor verschillende werkruimten.
* Als uw artefactbestanden om legitieme redenen erg groot worden, kunt u de &quot;hybride&quot; beslissingsmethode gebruiken. Deze methode staat u toe om het artefact in parallel te downloaden en alle vraag van doel API gaat over de draad tot het artefact heeft gedownload. Lees de sectie met aanbevolen procedures voor de &quot;Hybride&quot;-beslissingsmodus hieronder voor meer informatie over deze aanpak.
* Als u een toepassing voor één pagina hebt (SPA), [!DNL Adobe] Het wordt aangeraden om .js te laden en te initialiseren voordat u het JavaScript-hoofdbestand van uw toepassing laadt tijdens het laden van de eerste pagina. Met deze methode wordt het downloaden van artefacten veel eerder gestart, waardoor rendering sneller verloopt.

## Aanbevolen procedures wanneer de beslissingsmethode &quot;hybride&quot; is

Wanneer u &quot;hybride&quot; gebruikt als beslissingsmethode, wordt het artefact parallel gedownload. Tot het artefact wordt gedownload, om het even welke [!DNL Target] API-aanroepen gaan over de kabel, zelfs als de &#39;locaties&#39; geschikt zijn voor het apparaat. Dit gedrag is de standaardinstelling voor alles `getOffers()` roept en verstrekt de beste prestaties in de meeste situaties. Als u het standaardgedrag wijzigt van `getOffers()` door de `decisioningMethod` tot `on-device`, deze beste praktijken volgen om fouten te vermijden en de beste prestaties te verzekeren.

* Als u besluit te roepen `getOffers()` with `decisioningMethod` als `on-device` wanneer de pagina voor het eerst wordt geladen, moet u dit binnen de gebeurtenishandler &quot;ARTIFACT_DOWNLOAD_SUCCEEDED&quot; at.js doen om fouten te voorkomen. Als uw artefact zeer groot is, worden om het even welke &quot;plaatsen&quot;die deze benadering gebruiken teruggegeven slechts nadat het artefact volledig wordt gedownload, wat het teruggeven kan vertragen. [!DNL Adobe] Het verdient aanbeveling deze aanpak zelden te volgen. Volg de aanbevolen procedures om de grootte van artefacten te beperken in de bovenstaande sectie met aanbevolen procedures voor &quot;Op apparaat&quot; wanneer u deze aanpak gebruikt.
