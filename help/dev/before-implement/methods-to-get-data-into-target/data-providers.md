---
keywords: implementeren, implementeren, instellen, instellen, gegevensaanbieders
description: Gegevens ophalen in [!DNL Target] het gebruik van gegevensaanbieders.
title: Hoe krijg ik gegevens in [!DNL Target] Gegevensproviders gebruiken?
feature: Implementation
exl-id: 9971bd96-f736-4965-afe2-b4901c12d006
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# Gegevensleveranciers

Gegevensleveranciers zijn een mogelijkheid waarmee u gegevens van derden eenvoudig kunt doorgeven aan [!DNL Adobe Target].

>[!NOTE]
>
>Gegevensleveranciers vereisen at.js 1.3 of later.

## Indeling

De `window.targetGlobalSettings.dataProviders` het plaatsen is een serie van gegevensleveranciers.

Voor meer informatie over de structuur voor elke gegevensleverancier, zie [Gegevensleveranciers](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

## Voorbeelden van gebruiksgevallen

Verzamel gegevens van derden, zoals een weerservice, een DMP of zelfs uw eigen webservice. Vervolgens kunt u deze gegevens gebruiken om een publiek te maken, inhoud te benoemen en het profiel van de bezoeker te verrijken.

## Voordelen van de methode

Met deze instelling kunnen klanten gegevens verzamelen van externe gegevensleveranciers, zoals Demandbase, BlueKai en aangepaste services, en de gegevens doorgeven aan [!DNL Target] als mbox parameters in het globale mbox verzoek.

Het steunt de inzameling van gegevens van veelvoudige leveranciers via async en synchronisatieverzoeken.

Op deze manier kunt u flikkering van de standaardpagina-inhoud eenvoudig beheren en onafhankelijke time-outs opnemen voor elke provider om de invloed op de paginaprestaties te beperken

## Caveats

Als de gegevensleveranciers `window.targetGlobalSettings.dataProviders` asynchroon zijn, worden ze parallel uitgevoerd. De visitor-API-aanvraag wordt uitgevoerd in combinatie met toegevoegde functies `window.targetGlobalSettings.dataProviders` een minimale wachttijd toestaan.

at.js probeert niet om de gegevens in het voorgeheugen onder te brengen. Als de gegevensleverancier gegevens slechts één keer haalt, zou de gegevensleverancier ervoor moeten zorgen dat de gegevens in het voorgeheugen wordt opgeslagen en, wanneer de leveranciersfunctie wordt aangehaald, de geheim voorgeheugengegevens voor de tweede aanroeping dienen.

## Codevoorbeelden

Verschillende voorbeelden zijn te vinden in [Gegevensleveranciers](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

## Koppelingen naar relevante informatie

Documentatie: [Gegevensleveranciers](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)

## Trainingsvideo&#39;s:

* [Gegevensleveranciers gebruiken in Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/use-data-providers-to-integrate-third-party-data.html)
* [Gegevensleveranciers implementeren in Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/implement-data-providers-to-integrate-third-party-data.html)
