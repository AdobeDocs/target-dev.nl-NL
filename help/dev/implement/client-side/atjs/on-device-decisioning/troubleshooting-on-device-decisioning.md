---
keywords: implementatie, javascript bibliotheek, js, atjs, op apparatenbesluit, op apparatenbesluit, at.js, op apparaat, op apparaat, het oplossen van problemen, het oplossen van problemen, implementation2
description: Leer hoe u problemen kunt oplossen [!UICONTROL on-device decisioning] met de bibliotheek at.js.
title: Hoe los ik op-Apparaatbesluit met de JavaScript-bibliotheek at.js problemen op?
feature: at.js
exl-id: b9530cc7-5e83-4fdf-bde9-b2492e0861ff
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Problemen oplossen [!UICONTROL on-device decisioning] for at.js

Voer de volgende stappen uit om problemen op te lossen [!UICONTROL on-device decisioning] in [!UICONTROL Adobe Target] met de JavaScript-bibliotheek at.js:

## Stap 1: Laat het consolelogboek voor at.js toe

De URL-parameter toevoegen `mboxDebug=1` laat at.js toe om berichten in de console van uw browser te drukken.

Alle berichten bevatten een voorvoegsel &quot;AT:&quot;voor geschikt overzicht. Om ervoor te zorgen dat een artefact met succes is geladen, zou uw consolelogboek berichten gelijkend op het volgende moeten bevatten:

```
AT: LD.ArtifactProvider fetching artifact - https://assets.adobetarget.com/your-client-cide/production/v1/rules.json
AT: LD.ArtifactProvider artifact received - status=200
```

De volgende illustratie toont deze berichten in het consolelogboek:

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![Logbestand van console met artefactberichten](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/browser-console.png "Logbestand van console met artefactberichten"){zoomable="yes"}

## Stap 2: Verifieer de download van het regelartefact in het lusje van het Netwerk van uw browser

Open het tabblad Netwerk van uw browser.

Als u bijvoorbeeld DevTools wilt openen in Google Chrome:

1. Druk op Ctrl+Shift+J (Windows) of Command+Option+J (Mac).
1. Navigeer naar het tabblad Netwerk.
1. Filter uw vraag door sleutelwoord &quot;rules.json&quot;om ervoor te zorgen dat slechts de vertoningen van het artefactregelingendossier.

   Bovendien kunt u door &quot;/levering filteren|rules.json/&quot;om alle vraag van het Doel en artefact rules.json te tonen.

   ![Het tabblad Netwerk in Google Chrome](assets/rule-json.png)

## Stap 3: Verifieer de download van het regelartefact gebruikend at.js douanegebeurtenissen

De bibliotheek at.js verzendt twee nieuwe aangepaste gebeurtenissen ter ondersteuning [!UICONTROL on-device decisioning].

* `adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`
* `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`

U kunt zich abonneren om naar deze aangepaste gebeurtenissen in uw toepassing te luisteren en deze te activeren wanneer het downloaden van het bestand met artefactregels is gelukt of mislukt.

In het volgende voorbeeld ziet u een voorbeeld van code die luistert naar gebeurtenissen voor het downloaden van artefacten en mislukken:

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED, function(e) { 
  console.log("Artifact successfully downloaded", e.detail);
}, false);

document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_FAILED, function(e) { 
  console.log("Artifact failed to download", e.detail);
}, false);
```
