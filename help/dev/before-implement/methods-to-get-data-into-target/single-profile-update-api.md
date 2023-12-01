---
keywords: implementeren, implementeren, instellen, instellen, één profielupdate
description: Gegevens ophalen in [!DNL Target] met de API voor één profielupdate.
title: Hoe krijg ik gegevens in [!DNL Target] De Single Profile Update API gebruiken?
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
source-git-commit: af9db32d59bdf32f2b9fade267922803250377dd
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# Single Profile Update API

Bijna identiek aan [!UICONTROL Bulk Profile Update API] in [!DNL Adobe Target], maar één bezoekersprofiel wordt tegelijkertijd bijgewerkt, in lijn in de API-aanroep in plaats van met een .csv-bestand.

## Indeling

De bezoeker moet via de [!DNL Target] `mboxPC` waarde of `mbox3rdPartyId` waarde. De [!UICONTROL Experience Cloud ID] (ECID) wordt niet ondersteund.

## Voorbeelden van gebruiksgevallen

U wilt het profiel bijwerken van één bezoeker die een offlineactie uitvoert. De acties kunnen het bereiken van een callcenter omvatten, wordt een lening gefinancierd, gebruikend een loyaliteitskaart in opslag, die tot een kiosk toegang hebben, etc.

## Voordelen van de methode

* Geen limiet voor het aantal profielkenmerken.*
* Profielkenmerken die via de site worden verzonden, kunnen via de API worden bijgewerkt en omgekeerd.

## Caveats

* Limiet van 1.000.000 API-aanroepen (1 miljoen) per periode van 24 uur.
* Alleen profielen worden bijgewerkt. Kan geen profiel maken voor een potentiële gebruiker [!DNL Target] heeft nog niet gezien.
* Updates vinden meestal plaats binnen een uur, maar het kan 24 uur duren voordat ze worden gereflecteerd.

## Codevoorbeelden

GET en POST ondersteund.

```
https://CLIENT.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr1=0&profile.attr2=1...
```

## Bronnen

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)
