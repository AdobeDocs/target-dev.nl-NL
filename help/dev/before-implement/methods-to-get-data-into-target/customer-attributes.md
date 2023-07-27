---
keywords: implementeren, implementeren, instellen, instellen, klantkenmerken
description: Gegevens ophalen in [!DNL Target] het gebruik van klantkenmerken.
title: Hoe krijg ik gegevens in [!DNL Target] Klantkenmerken gebruiken?
feature: Implementation
exl-id: d05cdd38-ba7c-4f29-a0ef-ae68619e7617
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# Klantkenmerken

Met klantkenmerken kunt u gegevens van bezoekersprofielen uploaden via FTP naar de [!DNL Adobe Experience Cloud]. Gebruik de gegevens in [!DNL Adobe Analytics] en [!DNL Adobe Target].

Target Standard-klanten kunnen vijf kenmerken toepassen, [!DNL Target Premium] klanten kunnen 200 attributen toepassen.

## Indeling

Een CSV-bestand met [!DNL Experience Cloud] ID&#39;s (ECID&#39;s) en paren van kenmerknamen en -waarden worden geüpload via FTP of handmatig in de gebruikersinterface van Experience Cloud.

## Voorbeelden van gebruiksgevallen

Uw CRM of ander intern systeem slaat waardevolle informatie op u met wilt delen [!DNL Adobe Experience Cloud], inclusief [!DNL Target] en [!DNL Analytics].

## Voordelen van de methode

Tijdens het uploaden van klantgegevens wordt een profielvermelding voor die bezoeker in Doel gemaakt, zelfs als [!DNL Target] heeft de bezoeker nog niet gezien.

Dezelfde gegevens zijn automatisch beschikbaar in [!DNL Target] en [!DNL Analytics].

FTP kan een eenvoudigere implementatiemethode zijn dan API.

## Caveats

Target Standard-klanten kunnen vijf kenmerken toepassen, [!DNL Target Premium] klanten kunnen 200 attributen toepassen

Kan waarden alleen bijwerken via Customer Attributes, niet op pagina.

Vereist Experience Cloud ID-implementatie (ECID).

## Codevoorbeelden

Details vindt u in [Een bron voor klantkenmerken maken en het gegevensbestand uploaden](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html).

### Koppelingen naar relevante informatie

[Een bron voor klantkenmerken maken en het gegevensbestand uploaden](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html).
