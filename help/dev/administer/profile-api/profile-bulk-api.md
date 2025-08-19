---
title: Adobe Target Bulk Profile Update API
description: Leer hoe te om  [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] te gebruiken om de profielgegevens van veelvoudige bezoekers naar  [!DNL Target]  voor gebruik te verzenden in het richten.
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 0f38d109-5273-4f73-9488-80eca115d44d
source-git-commit: dae198fd8ef3fc8473ad31807c146802339b1832
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 0%

---

# [!DNL Adobe Target Bulk Profile Update API]

Met [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] kunt u gebruikersprofielen voor meerdere bezoekers van een website in bulk bijwerken met behulp van een batchbestand.

Met de [!UICONTROL Bulk Profile Update API] kunt u eenvoudig gedetailleerde gegevens van het bezoekersprofiel in de vorm van profielparameters voor veel gebruikers naar [!DNL Target] verzenden vanuit een externe bron. Externe bronnen kunnen systemen van het Beheer van de Verhouding van de Klant (CRM) of van het Verkooppunt (POS) omvatten, die gewoonlijk niet op een Web-pagina beschikbaar zijn.

| Versie | URL-voorbeeld | Functies |
| --- | --- | --- |
| v1 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/profile/batchUpdate` | Alleen ondersteuning voor bulkprofielupdate. |
| v2 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate` | <ul><li>Profiel maken indien niet gevonden.</li><li>Status per rij bijwerken.</li></ul> |

>[!NOTE]
>
>Versie 2 (v2) van de [!DNL Bulk Profile Update API] is de huidige versie. [!DNL Target] blijft echter versie 1 (v1) ondersteunen.
>
>* Als uw [!DNL Target] -implementatie [!DNL Experience Cloud ID] (ECID) gebruikt als een van de profiel-id&#39;s voor anonieme bezoekers, gebruikt u `pcId` niet als de sleutel in een batchbestand van versie 2 (v2). Het gebruik van `pcId` met v2 van [!DNL Bulk Profile Update API] is alleen bedoeld voor zelfstandige [!DNL Target] implementaties die niet afhankelijk zijn van ECID.
>
>* Als in uw implementatie ECID wordt gebruikt voor profielidentificatie en u `pcId` wilt gebruiken als de sleutel in het batchbestand, gebruikt u versie 1 (v1) van de API.
>
>* Als uw implementatie `thirdPartyId` gebruikt voor profielidentificatie, gebruikt u versie 2 (v2) van de API met `thirdPartyId` als sleutel.

## Voordelen van de [!UICONTROL Bulk Profile Update API]

* Geen limiet voor het aantal profielkenmerken.
* Profielkenmerken die via de site worden verzonden, kunnen via de API worden bijgewerkt en omgekeerd.

## Caveats

* Het batchbestand moet kleiner zijn dan 50 MB. Bovendien mag het totale aantal rijen niet groter zijn dan 500.000 rijen per upload.
* Updates vinden meestal plaats binnen een uur, maar het kan 24 uur duren voordat ze worden gereflecteerd.
* Er is geen limiet voor het aantal rijen dat of de rijen die u kunt uploaden over een periode van 24 uur in volgende batches. Nochtans, zou het innameproces tijdens kantooruren kunnen worden vertraagd om ervoor te zorgen dat andere processen efficiënt lopen.
* Opeenvolgende v2 vraag van de partijupdate zonder mbox vraag binnen tussen voor zelfde thirdPartyIds treedt de eigenschappen met voeten die in de eerste vraag van de partijupdate worden bijgewerkt.
* [!DNL Adobe] garandeert niet dat 100% van de gegevens van het batchprofiel in Target wordt gecontroleerd en bewaard en dus beschikbaar is voor gebruik bij het zoeken naar gegevens. In het huidige ontwerp bestaat de mogelijkheid dat een klein percentage gegevens (tot 0,1% van de grote productiepartijen) niet wordt opgetekend of bewaard.

## Batchbestand

Als u profielgegevens bulksgewijs wilt bijwerken, maakt u een batchbestand. Het batchbestand is een tekstbestand met waarden gescheiden door komma&#39;s die lijken op het volgende voorbeeldbestand.

``` ```
batch=pcId,param1,param2,param3,param4
123,value1
124,value1,,,value4
125,,value2
126,value1,value2,value3,value4
``` ```

>[!NOTE]
>
>De parameter `batch=` is vereist en moet aan het begin van het bestand worden opgegeven.

U verwijst dit bestand in de POST-aanroep naar [!DNL Target] servers om het bestand te verwerken. Houd rekening met het volgende wanneer u het batchbestand maakt:

* In de eerste rij van het bestand moeten kolomkoppen worden opgegeven.
* De eerste header moet een `pcId` of `thirdPartyId` zijn. [!UICONTROL Marketing Cloud visitor ID] wordt niet ondersteund. [!UICONTROL pcId] is een door [!DNL Target] gegenereerde bezoeker-id. `thirdPartyId` is een id die door de clienttoepassing is opgegeven en die via een mbox-aanroep als [!DNL Target] aan `mbox3rdPartyId` wordt doorgegeven. U moet hier naar dit item verwijzen als `thirdPartyId` .
* Parameters en waarden die u in het batchbestand opgeeft, moeten uit veiligheidsoverwegingen URL-gecodeerd zijn met UTF-8. Parameters en waarden kunnen naar andere randknooppunten worden doorgestuurd voor verwerking door HTTP-aanvragen.
* De parameters mogen alleen de notatie `paramName` hebben. Parameters worden weergegeven in [!DNL Target] als `profile.paramName` .
* Als u [!UICONTROL Bulk Profile Update API] v2 gebruikt, hoeft u niet alle parameterwaarden voor elke `pcId` op te geven. Profielen worden gemaakt voor `pcId` of `mbox3rdPartyId` die niet worden gevonden in [!DNL Target] . Als u v1 gebruikt, worden er geen profielen gemaakt voor ontbrekende pcIds of mbox3rdPartyIds.
* Het batchbestand moet kleiner zijn dan 50 MB. Bovendien mag het totale aantal rijen niet groter zijn dan 500.000. Deze limiet zorgt ervoor dat servers niet overstroomd raken met te veel verzoeken.
* U kunt meerdere bestanden verzenden. Het totaal van de rijen van alle bestanden die u op een dag verzendt, mag echter niet hoger zijn dan 1 miljoen voor elke client.
* Er is geen beperking op het aantal kenmerken dat u kunt uploaden. De totale grootte van de externe profielgegevens, die klantkenmerken, profiel-API, In-Mbox-profielparameters en profielscriptuitvoer bevatten, mag echter niet groter zijn dan 64 kB.
* Parameters en waarden zijn hoofdlettergevoelig.

## HTTP POST-aanvraag

Voer een HTTP POST-aanvraag in bij [!DNL Target] Edge-servers om het bestand te verwerken. Hier volgt een voorbeeld van een HTTP POST-aanvraag voor het bestand batch.txt met de opdracht curl:

``` ```
curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate
``` ```

Waarbij:

BATCH.TXT is de bestandsnaam. CLIENTCODE is de [!DNL Target] clientcode.

Als u de clientcode niet kent, klikt u in de [!DNL Target] gebruikersinterface op **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** . De clientcode wordt weergegeven in de sectie [!UICONTROL Account Details] .

### De reactie controleren

De API voor profielen retourneert de verzendstatus van de batch voor verwerking samen met een koppeling onder &quot;batchStatus&quot; voor een andere URL die de algemene status van de specifieke batchtaak weergeeft.

### Voorbeeld-API-reactie

De volgende code die is uitgesneden, is een voorbeeld van een API-reactie voor profielen:

```
<response>
    <success>true</success>
    <batchStatus>http://mboxedge45.tt.omtrdc.net/m2/demo/profile/batchStatus?batchId=demo-1701473848678-13029383</batchStatus>
    <message>Batch submitted for processing</message>
</response>
```

Als er een fout is, bevat de reactie `success=false` en een gedetailleerd bericht voor de fout.

### Standaardbatchstatusreactie

Een succesvol standaardantwoord wanneer op de bovenstaande `batchStatus` URL-koppeling wordt geklikt, ziet er als volgt uit:

```
<response><batchId>demo4-1701473848678-13029383</batchId><status>complete</status><batchSize>1</batchSize></response>
```

De verwachte waarden voor de statusvelden zijn:

| Status | Details |
| --- | --- |
| [!UICONTROL complete] | Het verzoek om de profielbatch-update is voltooid. |
| [!UICONTROL incomplete] | Het verzoek om de profielbatch-update wordt nog steeds verwerkt en niet voltooid. |
| [!UICONTROL stuck] | Het verzoek om de profielbatch-update blijft geldig en kan niet worden voltooid. |

### Gedetailleerde batchstatus URL-reactie

Een gedetailleerdere reactie kan worden opgehaald door een parameter `showDetails=true` door te geven aan de bovenstaande `batchStatus` url.

Bijvoorbeeld:

```
http://mboxedge45.tt.omtrdc.net/m2/demo/profile/batchStatus?batchId=demo-1701473848678-13029383&showDetails=true
```

#### Gedetailleerde respons

```
<response>
    <batchId>demo4-1701473848678-13029383</batchId>
    <status>complete</status>
    <batchSize>1</batchSize>
    <consumedCount>1</consumedCount>
    <successfulUpdates>1</successfulUpdates>
    <profilesNotFound>0</profilesNotFound>
    <failedUpdates>0</failedUpdates>
</response>
```
