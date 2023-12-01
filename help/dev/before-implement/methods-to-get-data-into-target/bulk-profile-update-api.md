---
keywords: API implementeren, implementeren, instellen, bulkprofielupdate
description: Gegevens ophalen in [!DNL Target] met de [!UICONTROL Bulk Profile Update API].
title: Hoe krijg ik gegevens in [!DNL Target] Met de [!UICONTROL Bulk Profile Update API]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: af9db32d59bdf32f2b9fade267922803250377dd
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---

# Bulkprofielupdate-API

Via API kunt u een .csv-bestand verzenden naar [!DNL Adobe Target] met updates voor bezoekersprofielen voor veel bezoekers. Elk bezoekersprofiel kan met veelvoudige in-pagina profielattributen in één vraag worden bijgewerkt.

Deze optie lijkt op [!UICONTROL customer attributes] met enkele verschillen:

* [!UICONTROL Customer attributes] gebruik een FTP-upload. De [!UICONTROL Target Bulk Profile Update API] gebruikt een HTTP POST-API.
* [!UICONTROL Customer attribute] gegevens kunnen worden gedeeld met [!DNL Analytics]. [!UICONTROL Bulk Profile Update] is alleen bruikbaar in [!DNL Target].
* [!UICONTROL Customer attributes] ondersteuning voor het maken van een profiel voor een gebruiker [!DNL Target] nog niet gezien.
   * [!UICONTROL Bulk Profile Update API] v2: u hoeft niet voor elke parameter alle waarden op te geven `pcId`. Profielen worden gemaakt voor alle `pcId` of `mbox3rdPartyId` dat niet wordt gevonden in [!DNL Target].
   * [!UICONTROL Bulk Profile Update API] v1: De [!UICONTROL Bulk Profile Update API] bestaande updates [!DNL Target] alleen profielen. Als u v1 gebruikt, worden er geen profielen gemaakt voor ontbrekende `pcIds` of `mbox3rdPartyIds`.
* [!UICONTROL Customer attributes] het gebruik van de [!UICONTROL Experience Cloud ID] (ECID) en het gebruik van een bron-id, zoals de CRM-id of de Loyalty-id.
* De [!UICONTROL Bulk Profile Update API] vereist of TNT ID of `mbox3rdPartyId`.
* U kunt de volgende tekens niet verzenden in `mbox3rdPartyID`: plusteken (+) en slash (/).

## Indeling

Het .csv-bestand moet naar elke bezoeker verwijzen via zijn [!DNL Target] PCID of `mbox3rdPartyId`. De [!UICONTROL Experience Cloud ID] (ECID) wordt niet ondersteund. Alle profielkenmerken/waarden worden gemaakt en bijgewerkt via de API. De indelingsgegevens zijn beschikbaar in de API-documentatie.

## Voorbeelden van gebruiksgevallen

Uw CRM of ander intern systeem slaat waardevolle gegevens over uw bezoekers op die u constant in wilt bijwerken [!DNL Target]zonder de profielgegevens in uw pagina-implementatie toegankelijk te maken.

## Voordelen van de methode

* Geen limiet voor het aantal profielkenmerken.
* Profielkenmerken die via de site worden verzonden, kunnen via de API worden bijgewerkt en omgekeerd.

## Caveats

* Het batchbestand moet kleiner zijn dan 50 MB. Bovendien mag het totale aantal rijen niet groter zijn dan 500.000 rijen per upload.
* Updates vinden meestal plaats binnen een uur, maar het kan 24 uur duren voordat ze worden gereflecteerd.
* Er is geen limiet voor het aantal rijen dat of de rijen die u kunt uploaden over een periode van 24 uur in volgende batches. Nochtans, zou het innameproces tijdens kantooruren kunnen worden vertraagd om ervoor te zorgen dat andere processen efficiënt lopen.
* Opeenvolgende V2 vraag van de partijupdate zonder mbox vraag binnen tussen voor het zelfde `thirdPartyIds` Overschrijf de eigenschappen die in de eerste vraag van de partijupdate worden bijgewerkt.

## Bronnen

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)