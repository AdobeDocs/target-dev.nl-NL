---
keywords: implementeren, implementeren, instellen, instellen, bulkprofielupdate
description: Gegevens ophalen in [!DNL Target] met de API voor bulkprofielupdate.
title: Hoe krijg ik gegevens in [!DNL Target] De API voor updates van bulkprofielen gebruiken?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 3ae2391dea9994c0ddc1df39d74cccf6e067c1a4
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Bulkprofielupdate-API

Via API kunt u een .csv-bestand verzenden naar [!DNL Adobe Target] met updates voor bezoekersprofielen voor veel bezoekers. Elk bezoekersprofiel kan met veelvoudige in-pagina profielattributen in één vraag worden bijgewerkt.

Deze optie lijkt op Customer Attributes met een paar verschillen:

* Klantkenmerken gebruiken een FTP-upload terwijl de [!UICONTROL Target Bulk Profile Update API] gebruikt een HTTP POST-API.
* Gegevens van klantkenmerken kunnen worden gedeeld met [!DNL Analytics]. [!UICONTROL Bulk Profile Update] is alleen bruikbaar in Doel.
* Klantenkenmerken ondersteunen het maken van een profiel voor een gebruiker [!DNL Target] nog niet gezien. De API voor updates van bulkprofielen werkt bestaande [!DNL Target] alleen profielen.
* Klantkenmerken vereisen het gebruik van de Experience Cloud-id (ECID) en het gebruik van een bron-id, zoals de CRM-id of de Loyalty-id.
* De API voor het bijwerken van een bulkprofiel vereist de TNT-id of de `mbox3rdPartyId`.
* U kunt de volgende tekens niet verzenden in `mbox3rdPartyID`: plusteken (+) en slash (/).

## Indeling

Het .csv-bestand moet elke bezoeker via zijn of haar [!DNL Target] PCID of `mbox3rdPartyId`. De Experience Cloud-id (ECID) wordt niet ondersteund. Alle profielkenmerken/waarden worden gemaakt en bijgewerkt via de API. De indelingsgegevens zijn beschikbaar in de API-documentatie.

## Voorbeelden van gebruiksgevallen

Uw CRM of ander intern systeem slaat waardevolle gegevens over uw bezoekers op die u constant in Doel wilt bijwerken, zonder de profielgegevens in uw paginaimplementatie bloot te stellen.

## Voordelen van de methode

Geen limiet voor het aantal profielkenmerken.

Profielkenmerken die via de site worden verzonden, kunnen via de API worden bijgewerkt en andersom.

## Caveats

Het batchbestand moet kleiner zijn dan 50 MB. Bovendien mag het totale aantal rijen niet groter zijn dan 500.000 rijen per upload.

De updates komen over het algemeen binnen onder één uur voor, maar kunnen tot 24 uur vergen om worden weerspiegeld

Er geldt geen limiet voor het aantal rijen dat of de rijen die u kunt uploaden over een periode van 24 uur in volgende batches. Nochtans, zou het innameproces tijdens kantooruren kunnen worden vertraagd om ervoor te zorgen dat andere processen efficiënt lopen.

Opeenvolgend [V2 batch-updateaanroepen](https://developers.adobetarget.com/api/#updating-profiles) zonder mbox vraag binnen tussen voor zelfde thirdPartyIds treedt de eigenschappen met voeten die in de eerste vraag van de partijupdate worden bijgewerkt.

## Codevoorbeelden

Zie [Profielen bijwerken](https://developers.adobetarget.com/api/#updating-profiles).

### Koppelingen naar relevante informatie

[Profielen bijwerken](https://developers.adobetarget.com/api/#updating-profiles)
