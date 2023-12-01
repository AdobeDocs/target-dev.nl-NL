---
keywords: API implementeren, implementeren, instellen, bulkprofielupdate
description: Gegevens ophalen in [!DNL Target] met de [!UICONTROL Bulk Profile Update API].
title: Hoe krijg ik gegevens in [!DNL Target] Met de [!UICONTROL Bulk Profile Update API]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 946e9431e6bde30f564b4ba1a4cf0a78d8c5c6bf
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Bulkprofielupdate-API

De [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] Hiermee kunt u gebruikersprofielen voor meerdere bezoekers van een website in bulk bijwerken met een batchbestand.

Met de [!UICONTROL Bulk Profile Update API], kunt u gedetailleerde gegevens van het bezoekersprofiel in de vorm van profielparameters voor vele gebruikers gemakkelijk verzenden aan [!DNL Target] van een externe bron. Externe bronnen kunnen systemen van het Beheer van de Verhouding van de Klant (CRM) of van het Verkooppunt (POS) omvatten, die gewoonlijk niet op een Web-pagina beschikbaar zijn.

Contrast de [!UICONTROL Bulk Profile Update API] met de [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## [!UICONTROL Customer attributes] tegen de [!UICONTROL Bulk Profile Update API]

Deze optie lijkt op [[!UICONTROL customer attributes]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md) met enkele verschillen:

* [!UICONTROL Customer attributes] gebruik een FTP-upload. De [!UICONTROL Target Bulk Profile Update API] gebruikt een HTTP POST-API.
* [!UICONTROL Customer attribute] gegevens kunnen worden gedeeld met [!DNL Analytics]. De [!UICONTROL Bulk Profile Update] is alleen bruikbaar in [!DNL Target].
* [!UICONTROL Customer attributes] ondersteuning voor het maken van een profiel voor een gebruiker [!DNL Target] nog niet gezien.
   * [!UICONTROL Bulk Profile Update API] v2: u hoeft niet voor elke parameter alle waarden op te geven `pcId`. Profielen worden gemaakt voor alle `pcId` of `mbox3rdPartyId` dat niet wordt gevonden in [!DNL Target].
   * [!UICONTROL Bulk Profile Update API] v1: De [!UICONTROL Bulk Profile Update API] bestaande updates [!DNL Target] alleen profielen. Als u v1 gebruikt, worden er geen profielen gemaakt voor ontbrekende `pcIds` of `mbox3rdPartyIds`.
* [!UICONTROL Customer attributes] het gebruik van de [!UICONTROL Experience Cloud ID] (ECID) en het gebruik van een bron-id, zoals de CRM-id of de Loyalty-id.
* De [!UICONTROL Bulk Profile Update API] vereist of TNT ID of `mbox3rdPartyId`.
* U kunt de volgende tekens niet verzenden in `mbox3rdPartyID`: plusteken (+) en slash (/).

## Bronnen

Zie voor meer informatie:

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)