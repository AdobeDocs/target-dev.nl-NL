---
title: Adobe Target Bulk Profile Update API
description: Leren gebruiken [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] om profielgegevens van meerdere bezoekers te verzenden naar [!DNL Target] voor gebruik bij doelwitten.
feature: APIs/SDKs
contributors: https://github.com/icaraps
source-git-commit: a6f47c99cfc419771c1a6674990c415a2035ab4e
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# [!DNL Adobe Target Bulk Profile Update API]

De [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] Hiermee kunt u gebruikersprofielen voor meerdere bezoekers van een website in bulk bijwerken met een batchbestand.

Met de [!UICONTROL Bulk Profile Update API], kunt u gedetailleerde gegevens van het bezoekersprofiel in de vorm van profielparameters voor vele gebruikers gemakkelijk verzenden aan [!DNL Target] van een externe bron. Externe bronnen kunnen systemen van het Beheer van de Verhouding van de Klant (CRM) of van het Verkooppunt (POS) omvatten, die gewoonlijk niet op een Web-pagina beschikbaar zijn.

| Versie | URL-voorbeeld | Functies |
| --- | --- | --- |
| v1 | `http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/profile/batchUpdate` | Alleen ondersteuning voor bulkprofielupdate. |
| v2 | `http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/v2/profile/batchUpdate` | <ul><li>Profiel maken indien niet gevonden.</li><li>Status per rij bijwerken.</li></ul> |

>[!NOTE]
>
>Versie 2 van de [!UICONTROL Bulk Profile Update API] is de huidige versie. Maar [!DNL Target] ondersteunt nog steeds versie 1 (v1).

## Voordelen van de Bulk Profile Update API

* Geen limiet voor het aantal profielkenmerken.
* Profielkenmerken die via de site worden verzonden, kunnen via de API worden bijgewerkt en omgekeerd.

## Caveats

* Het batchbestand moet kleiner zijn dan 50 MB. Bovendien mag het totale aantal rijen niet groter zijn dan 500.000 rijen per upload.
* Er is geen limiet voor het aantal rijen dat of de rijen die u kunt uploaden over een periode van 24 uur in volgende batches. Nochtans, zou het innameproces tijdens kantooruren kunnen worden vertraagd om ervoor te zorgen dat andere processen efficiënt lopen.
* Opeenvolgende v2 vraag van de partijupdate zonder mbox vraag binnen tussen voor zelfde thirdPartyIds treedt de eigenschappen met voeten die in de eerste vraag van de partijupdate worden bijgewerkt.
* [!DNL Adobe] garandeert niet dat 100% van de gegevens van het batchprofiel in Target zal worden bewaard en bewaard en dus beschikbaar zal zijn voor gebruik bij het bepalen van doelwitten. In het huidige ontwerp bestaat de mogelijkheid dat een klein percentage gegevens (tot 0,1% van de grote productiepartijen) niet wordt opgetekend of bewaard.

## Batchbestand

Als u profielgegevens bulksgewijs wilt bijwerken, maakt u een batchbestand. Het batchbestand is een tekstbestand met waarden gescheiden door komma&#39;s die lijken op het volgende voorbeeldbestand.

``````
batch=pcId, param1, param2, param3, param4 123, value1 124, value1,,, value4 125,, value2 126, value1, value2, value3, value4
``````

U verwijst dit dossier in de vraag van de POST naar [!DNL Target] -servers om het bestand te verwerken. Houd rekening met het volgende wanneer u het batchbestand maakt:

* In de eerste rij van het bestand moeten kolomkoppen worden opgegeven.
* De eerste header moet een van de `pcId` of `thirdPartyId`. De [!UICONTROL Marketing Cloud visitor ID] wordt niet ondersteund. [!UICONTROL pcId] is een [!DNL Target]-generated bezoekerID. `thirdPartyId` is een id die is opgegeven door de clienttoepassing en die wordt doorgegeven aan [!DNL Target] door een mbox vraag zoals `mbox3rdPartyId`. Hier moet naar worden verwezen als `thirdPartyId`.
* Parameters en waarden die u in het batchbestand opgeeft, moeten uit veiligheidsoverwegingen URL-gecodeerd zijn met UTF-8. Parameters en waarden kunnen naar andere randknooppunten worden doorgestuurd voor verwerking door HTTP-aanvragen.
* De parameters moeten in het formaat zijn `paramName` alleen. Parameters worden weergegeven in [!DNL Target] als `profile.paramName`.
* Als u [!UICONTROL Bulk Profile Update API] v2, hoeft u niet voor elke parameter alle waarden op te geven `pcId`. Profielen worden gemaakt voor alle `pcId` of `mbox3rdPartyId` dat niet wordt gevonden in [!DNL Target]. Als u v1 gebruikt, worden er geen profielen gemaakt voor ontbrekende pcIds of mbox3rdPartyIds.
* Het batchbestand moet kleiner zijn dan 50 MB. Bovendien mag het totale aantal rijen niet groter zijn dan 500.000. Deze limiet zorgt ervoor dat servers niet overstroomd raken met te veel verzoeken.
* U kunt meerdere bestanden verzenden. Het totaal van de rijen van alle bestanden die u op een dag verzendt, mag echter niet hoger zijn dan 1 miljoen voor elke client.
* Er is geen limiet voor het aantal kenmerken dat u uploadt. De totale grootte van een profiel, inclusief systeemgegevens, mag echter niet groter zijn dan 2000 kB. [!DNL Adobe] U wordt aangeraden minder dan 1000 kB opslagruimte te gebruiken voor profielkenmerken.
* Parameters en waarden zijn hoofdlettergevoelig.

## HTTP POST request

Een HTTP-POST aanvragen om [!DNL Target] Edge-servers om het bestand te verwerken. Hier volgt een voorbeeld van een HTTP-POST-aanvraag voor het bestand batch.txt met de opdracht curl:

``````
curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate
``````

Waarbij:

BATCH.TXT is de bestandsnaam. CLIENTCODE is de [!DNL Target] clientcode.

Als u uw cliëntcode niet kent, in [!DNL Target] gebruikersinterface klikken **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**. De clientcode wordt weergegeven in het dialoogvenster [!UICONTROL Account Details] sectie.

### Inspect: het antwoord

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

Als er een fout optreedt, bevat de reactie `success=false` en een gedetailleerd bericht voor de fout.

### Standaardbatchstatusreactie

Een geslaagde standaardreactie bij het bovenstaande `batchStatus` Als u op een URL-koppeling klikt, ziet u er als volgt uit:

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

Een meer gedetailleerde reactie kan worden opgehaald door een parameter door te geven `showDetails=true` aan de `batchStatus` URL hierboven.

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
