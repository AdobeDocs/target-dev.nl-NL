---
title: Begrijp het op apparaat beslissingsregelartefact
description: Leer hoe u de vervorming van de regel gebruikt. Dit is een JSON-weergave van uw [!DNL Adobe Target] [!UICONTROL on-device decisioning] activiteiten.
feature: APIs/SDKs
exl-id: 3dfb08df-eaa9-43d4-b009-e5f64c3a96d7
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Overzicht van artikelen

De regel-artefact is een JSON-weergave van uw [!DNL Adobe Target] [!UICONTROL on-device decisioning] activiteiten. Het wordt gegenereerd door [!DNL Adobe Target] en doorgegeven aan de Akamai CDN om er zeker van te zijn dat er een regelartefact beschikbaar is die zo dicht mogelijk bij uw eindgebruikers ligt. Het bevat metagegevens die zorgen voor een nauwkeurige uitvoering en levering van uw activiteiten, terwijl ook realtime analyses mogelijk zijn via het bijhouden van gebeurtenissen. De [!DNL Adobe Target] SDKs kan op een manier worden gevormd die voor automatisch beheer van het regelartefact toestaat, waardoor het volgens een user-specified tijdinterval kan worden gedownload of worden bijgewerkt. Bovendien kunt u uw eigen lokale exemplaar van het regelartefact ook handhaven gebruikend een verdeeld geheugen caching systeem zoals [Gecentreerd](https://memcached.org/) om het [!DNL Adobe Target] SDK, zodat uw stateless servers aanvragen direct kunnen indienen. Raadpleeg de volgende hulplijnen voor meer informatie over deze opties:

* [Het artikel van de Regel automatisch downloaden, opslaan en bijwerken via [!DNL Adobe Target] SDK](rule-artifact-sdk.md)
* [Het Artefact van de Regel downloaden, opslaan en bijwerken via JSON Payload](rule-artifact-json.md)

## Artefact van voorbeeldregel

Klik hier voor een voorbeeld van het [regelartefact](rule-artifact-example.md).

## Hoe te om het regelartefact voor uw cliënt te bekijken

Als u sporen inschakelt, wordt aanvullende informatie van [!DNL Adobe Target] met betrekking tot het regelartefact, met name URL.

1. Navigeer naar de interface Doel.

   &lt;!— Afbeelding-target-ui-1.png invoegen —>
   ![alternatieve afbeelding](assets/asset-rule-artifact-1.png)

1. Navigeren naar **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** en klik op **[!UICONTROL Generate New Authorization Token]**.

   &lt;!— Afbeelding-target-ui-2.png invoegen —>
   ![alternatieve afbeelding](assets/asset-rule-artifact-2.png)

1. Kopieer het nieuw gegenereerde machtigingstoken naar het klembord en voeg deze toe aan uw doelverzoek.

   ```javascript {line-numbers="true"}
   const request = {
     trace: {
       authorizationToken: '88f1a924-6bc5-4836-8560-2f9c86aeb36b'
     },
     execute: {
       mboxes: [{
         address: getAddress(req),
         name: "node-sdk-mbox"
       }]
   }};
   ```

1. Output het Spoor van het Doel via de terminal om details over het artefact te bekijken. De URL is toegankelijk via de `artifactLocation` variabele.

   ```
   "trace": {
     "clientCode": "your-client-code",
     "artifact": {
       "artifactLocation": "https://assets.adobetarget.com/your-client-code/production/v1/rules.bin",
       "pollingInterval": 300000,
       "pollingHalted": false,
       "artifactVersion": "1.0.0",
       "artifactRetrievalCount": 10,
       "artifactLastRetrieved": "2020-09-20T00:09:42.707Z",
        "clientCode": "your-client-code",
      "environment": "production",
       "generatedAt": "2020-09-22T17:17:59.783Z"
     },
   ```
