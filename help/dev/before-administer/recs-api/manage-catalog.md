---
title: Recommendations-catalogus beheren met API's
description: Stappen die nodig zijn om Adobe Target API's te gebruiken voor het maken, bijwerken, opslaan, ophalen en verwijderen van entiteiten in uw Recommendations-catalogus.
feature: APIs/SDKs, Recommendations, Administration & Configuration
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: aea82607-cde4-456a-8dfb-2967badce455
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 1%

---

# Uw Recommendations-catalogus beheren met behulp van API&#39;s

Terwijl u ervoor zorgt dat u voldoet aan de [vereisten voor het gebruik van de Recommendations API](/help/dev/before-administer/recs-api/overview.md#prerequisites), hebt u geleerd hoe te [een toegangstoken genereren](/help/dev/before-administer/configure-authentication.md) de JWT-verificatiestroom gebruiken om de [!DNL Adobe Target] Admin API&#39;s op de [Adobe Developer Console](https://developer.adobe.com/console/home).

U kunt nu de opdracht [Recommendations API&#39;s](https://developers.adobetarget.com/api/recommendations/) om items toe te voegen, bij te werken of te verwijderen uit uw catalogus met aanbevelingen. Net als bij de andere Adobe Target Admin API&#39;s is verificatie vereist voor de Recommendations API&#39;s.

>[!NOTE]
>
>Verzend de **[!UICONTROL IMS: JWT Generate + Auth via User Token]** verzoek wanneer u uw toegangstoken voor authentificatie moet verfrissen, aangezien het na 24 uren verloopt. Zie [Adobe API-verificatie configureren](../configure-authentication.md) voor instructies.

![JWT3ff](assets/configure-io-target-jwt3ff.png)

Haal voordat u verdergaat de [Recommendations Postman-collectie](https://developers.adobetarget.com/api/recommendations/#section/Postman).

## Items maken en bijwerken met de API Entiteiten opslaan

Als u de Recommendations-productdatabase wilt vullen met behulp van de API in plaats van een CSV-productfeed of Target-aanvraag die wordt gestart op productpagina&#39;s, gebruikt u de optie [Entiteiten-API opslaan](https://developers.adobetarget.com/api/recommendations/#operation/saveEntities). Met deze aanvraag wordt een item toegevoegd of bijgewerkt in één doelomgeving. De syntaxis is:

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

Bijvoorbeeld, sparen Entiteiten kunnen worden gebruikt om punten bij te werken wanneer bepaalde drempels worden voldaan-zoals drempels voor inventaris of prijs-om die punten te markeren en hen te verhinderen worden geadviseerd.

1. Navigeren naar **[!UICONTROL Target]** > **[!UICONTROL Setup]** > **[!UICONTROL Hosts]** > **[!UICONTROL CONTROL Environments]** om identiteitskaart van het Milieu van het Doel te verkrijgen waarin u een punt wilt toevoegen of bijwerken.

   ![SaveEntities1](assets/SaveEntities01.png)

1. Verifiëren `TENANT_ID` en `API_KEY` verwijzen naar de eerder vastgestelde Postman-omgevingsvariabelen. Gebruik de onderstaande afbeelding om deze te vergelijken. Wijzig zo nodig de koppen en het pad in de API-aanvraag, zodat deze overeenkomen met de waarden in de onderstaande afbeelding.

   ![SaveEntities3](assets/SaveEntities03.png)

1. Voer uw JSON in als **ruw** code in de **Lichaam**. Vergeet niet uw milieu-id op te geven met de `environment` variabele. (In het onderstaande voorbeeld is de milieu-id 6781.)

   ![SaveEntities4.png](assets/SaveEntities04.png)

   Hieronder ziet u een voorbeeld van JSON waarmee entiteit.id kit2001 wordt toegevoegd aan de bijbehorende entiteitswaarden voor een product van Toaster Oven, in omgeving 6781.

   ```
       {
       "entities": [{
               "name": "Toaster Oven",
               "id": "kit2001",
               "environment": 6781,
               "categories": [
                   "housewares:appliances"
               ],
               "attributes": {
                   "inventory": 77,
                   "margin": 23,
                   "message": "crashing helicopter",
                   "pageUrl": "www.foobar.foo.com/helicopter.html",
                   "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                  "value": 19.2
               }
           }]
       }
   ```

1. Klik op **[!UICONTROL Send]**. U dient het volgende antwoord te ontvangen.

   ![SaveEntities5.png](assets/SaveEntities05.png)

   Het JSON-object kan worden geschaald om meerdere producten te verzenden. In deze JSON worden bijvoorbeeld twee entiteiten opgegeven.

   ```
       {
           "entities": [{
                   "name": "Toaster Oven",
                   "id": "kit2001",
                   "environment": 6781,
                   "categories": [
                       "housewares:appliances"
                   ],
                   "attributes": {
                       "inventory": 89,
                       "margin": 11,
                       "message": "Toaster Oven",
                       "pageUrl": "www.foobar.foo.com/helicopter.html",
                       "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                       "value": 102.5
                   }
               },
               {
                   "name": "Blender",
                   "id": "kit2002",
                   "environment": 6781,
                   "categories": [
                       "housewares:appliances"
                   ],
                   "attributes": {
                       "inventory": 36,
                       "margin": 5,
                       "message": "Blender",
                       "pageUrl": "www.foobar.foo.com/helicopter.html",
                       "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                       "value": 54.5
                   }
               }
           ]
       }
   ```

1. Nu is het jouw beurt! Gebruik de **[!UICONTROL Save Entities]** API om de volgende items aan uw catalogus toe te voegen. Gebruik het JSON-voorbeeld hierboven als beginpunt. (U moet de JSON uitbreiden tot extra entiteiten.)

   ![SaveEntities6.png](assets/SaveEntities06.png)

Deze laatste twee items horen niet bij elkaar. Laten we ze controleren met de **[!UICONTROL Get Entity]** API, en indien nodig, schrapt hen gebruikend **[!UICONTROL Delete Entities]** API.

## Itemdetails ophalen met de Get Entiteit API

Om de details van een bestaand punt terug te winnen, gebruik [EntiteitsAPI ophalen](https://developers.adobetarget.com/api/recommendations/#operation/getEntity). De syntaxis is:

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

De gegevens van de entiteit kunnen slechts voor één enkele entiteit tegelijkertijd worden teruggewonnen. Met Entiteit ophalen kunt u controleren of er updates zijn gemaakt in de catalogus zoals u had verwacht, of kunt u de inhoud van de catalogus op een andere manier controleren.

1. Geef in de API-aanvraag de id van de entiteit op met de variabele `entityId`. Het volgende voorbeeld zal details voor de entiteit terugkeren waarvan entiteitId=kit2004.

   ![GetEntity1](assets/GetEntity1.png)

1. Verifiëren `TENANT_ID` en `API_KEY` verwijzen naar de eerder vastgestelde Postman-omgevingsvariabelen. Gebruik de onderstaande afbeelding om deze te vergelijken. Wijzig zo nodig de koppen en het pad in de API-aanvraag, zodat deze overeenkomen met de waarden in de onderstaande afbeelding.

   ![GetEntity2](assets/GetEntity2.png)

1. Verzend de aanvraag.

   ![GetEntiteit3](assets/GetEntity3.png)
Als er een fout optreedt die aangeeft dat de entiteit niet is gevonden, zoals in het bovenstaande voorbeeld wordt getoond, controleert u of u de aanvraag naar de juiste doelomgeving verzendt.



   >[!NOTE]
   >
   >Als geen milieu uitdrukkelijk wordt gespecificeerd, krijg de pogingen van de Entiteit om de entiteit van uw te krijgen [standaardomgeving](https://experienceleague.adobe.com/docs/target/using/administer/environments.html) alleen. Als u van om het even welke milieu buiten uw standaardomgeving wenst te trekken, moet u milieu-identiteitskaart specificeren.

1. Voeg zo nodig de `environmentId` en de aanvraag opnieuw verzenden.

   ![GetEntity4](assets/GetEntity4.png)

1. Nog een verzenden **[!UICONTROL Get Entity]** verzoek, dit keer om de entiteit te inspecteren waarvan entiteitId=kit2005.

   ![GetEntity5](assets/GetEntity5.png)

Stel dat u besluit dat deze entiteiten uit de catalogus moeten worden verwijderd. Laten we de **[!UICONTROL Delete Entities]** API.

## Items verwijderen met de API Entiteiten verwijderen

Als u items uit uw catalogus wilt verwijderen, gebruikt u de [Entiteiten-API verwijderen](https://developers.adobetarget.com/api/recommendations/#operation/deleteEntities). De syntaxis is:

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
>
>Met de API Entiteiten verwijderen verwijdert u entiteiten waarnaar wordt verwezen door de id&#39;s die u opgeeft. Als er geen id&#39;s voor entiteiten zijn opgegeven, worden alle entiteiten in de opgegeven omgeving verwijderd. Als er geen milieu-id is opgegeven, worden entiteiten uit alle omgevingen verwijderd. Wees voorzichtig!

1. Navigeren naar **[!UICONTROL Target]** > **[!UICONTROL Setup]** > **[!UICONTROL Hosts]** > **[!UICONTROL Environments]** om identiteitskaart van het Milieu van het Doel te verkrijgen waaruit u punten wilt schrappen.

   ![DeleteEntities1](assets/SaveEntities01.png)

1. Geef in de API-aanvraag de entiteit-id&#39;s op van de entiteiten die u wilt verwijderen met behulp van de syntaxis `&ids=[comma-delimited-entity-ids]` (een queryparameter). Wanneer u meerdere entiteiten verwijdert, scheidt u de id&#39;s met komma&#39;s.

   ![DeleteEntities2](assets/DeleteEntities2.png)

1. De milieu-id opgeven met de syntaxis `&environment=[environmentId]`anders worden entiteiten in alle omgevingen verwijderd.

   ![DeleteEntities3](assets/DeleteEntities3.png)

1. Verifiëren `TENANT_ID` en `API_KEY` verwijzen naar de eerder vastgestelde Postman-omgevingsvariabelen. Gebruik de onderstaande afbeelding om deze te vergelijken. Wijzig zo nodig de koppen en het pad in de API-aanvraag, zodat deze overeenkomen met de waarden in de onderstaande afbeelding.

   ![DeleteEntities4](assets/DeleteEntities4.png)

1. Verzend de aanvraag.

   ![DeleteEntities5](assets/DeleteEntities5.png)

1. De resultaten verifiëren met **[!UICONTROL Get Entity]**, die nu moet aangeven welke verwijderde entiteiten niet kunnen worden gevonden.

   ![DeleteEntities6](assets/DeleteEntities6.png)

   ![DeleteEntities6](assets/DeleteEntities7.png)

Gefeliciteerd! U kunt nu de Recommendations API&#39;s gebruiken om gegevens over de entiteiten in uw catalogus te maken, bij te werken, te verwijderen en op te halen. In de volgende sectie leert u hoe u aangepaste criteria kunt beheren.

&lt;!— [Volgende &quot;Aangepaste criteria beheren&quot; >](manage-custom-criteria.md) —>
