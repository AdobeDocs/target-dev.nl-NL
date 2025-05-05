---
title: Overzicht Adobe Target Admin API
description: Overzicht van de [!DNL Adobe Target Admin API]
exl-id: 1168d376-c95b-4c5a-b7a2-c7815799a787
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 0%

---

# Overzicht van Admin API voor doelbeheerder

Dit artikel biedt een overzicht van de achtergrondinformatie die nodig is om deze te begrijpen en te gebruiken [!DNL Adobe Target Admin API]is gelukt. In de volgende inhoud wordt ervan uitgegaan dat u begrijpt hoe [verificatie configureren](../configure-authentication.md) for [!DNL Adobe Target Admin API]s.

>[!NOTE]
>
>Indien u wilt toedienen [!DNL Target] via de interface [rubriek van de *Adobe Target Business Practice Guide*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=nl-NL).
>
>De API&#39;s voor beheerders en profiel-API&#39;s worden vaak gezamenlijk genoemd (&quot;Admin en Profile API&#39;s&quot;), maar kunnen ook afzonderlijk worden vermeld (&quot;Admin API&#39;s&quot; en &quot;Profile API&#39;s&quot;). De Recommendations API is een specifieke implementatie van een [!DNL Target] Admin API.

## Voordat u begint

In alle codevoorbeelden die voor [Admin API&#39;s](../../administer/admin-api/admin-api-overview-new.md)vervangen {tenant} met uw huurderswaarde, `your-bearer-token` met de toegangstoken die u met uw JWT produceert en `your-api-key` met uw API-sleutel vanuit de [Adobe Developer Console](https://developer.adobe.com/console/home). Lees voor meer informatie over huurders en JWTs het artikel over hoe te [verificatie configureren](../configure-authentication.md) voor Adobe [!DNL Target] Admin API&#39;s.

## Versioning

Aan alle API&#39;s is een versie gekoppeld. Het is belangrijk om de juiste versie van de API te verstrekken u wilt gebruiken.

Als het verzoek een lading (POST of PUT) bevat, `Content-Type` header van het verzoek wordt gebruikt om de versie op te geven.

Als het verzoek geen lading (GET, DELETE of OPTIONS) bevat, `Accept` header wordt gebruikt om de versie op te geven.

Als een versie niet wordt verstrekt, zal de vraag aan V1 (application/vnd.adobe.target.v1+json) in gebreke blijven.

>[!NOTE]
>
>Als de juiste versie niet is opgegeven, bijvoorbeeld als u een V2-payload gebruikt maar de header Inhoudstype niet opgeeft, reageert de API met een niet-ondersteunde fout als de API niet achterwaarts compatibel is.

Foutbericht voor niet-ondersteunde functies

```
{
    "httpStatus": 406,
    "requestId": "8752b736-cf71-4d81-86c3-94be2b5ae648",
    "requestTime": "2018-02-02T21:39:06.405Z",
    "errors": [
        {
            "errorCode": "Unsupported.Feature",
            "message": "Unsupported features detected"
        }
    ]
}
```

Admin Postman Collection

Postman is een toepassing waarmee het eenvoudig is API-aanroepen te starten. Dit [Postman-verzameling voor Admin API](https://developers.adobetarget.com/api/#admin-postman-collection) bevat alle API-aanroepen van Target die verificatie vereisen met Activiteiten, Soorten publiek, Aanbiedingen, Rapporten, Mboxen en Omgevingen

## Antwoordcodes

Hier volgen de algemene responscodes voor de API&#39;s voor doelbeheer.

| Status | Betekenis | Beschrijving |
| --- | --- | --- |
| 200 | [OK](https://www.rfc-editor.org/rfc/rfc7231#section-6.3.1) | OK |  |
| 400 | [Ongeldig verzoek](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.1) | Onjuist verzoek. Waarschijnlijk zijn de gegevens in het verzoek ongeldig. |  |
| 401 | [Ongeautoriseerd](https://www.rfc-editor.org/rfc/rfc7235#section-3.1) | De gebruiker mag deze bewerking niet uitvoeren. |  |
| 403 | [Verboden](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.3) | Toegang tot deze resource is verboden. |  |
| 404 | [Niet gevonden](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.4) | De resource waarnaar wordt verwezen, is niet gevonden. |  |

## Activiteiten

Met een activiteit kunt u inhoud voor uw gebruikers testen of aanpassen. De activiteiten kunnen een van de volgende soorten activiteiten zijn:

* [A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=nl-NL)
* [Gericht op ervaring (XT)](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html?lang=nl-NL)
* [Recommendations](https://experienceleague.adobe.com/docs/target/using/activities/recommendations-activity.html?lang=nl-NL)
* [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html?lang=nl-NL)
* [MVT (Multivariate Test)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html?lang=nl-NL)

## Batchupdates

Meerdere Admin API&#39;s kunnen als één batchaanvraag worden uitgevoerd.

### Uitvoeren Vraag in Batch

`POST /{tenant}/target/batch`

Stapel veelvoudige API vraag samen en voer hen in één enkele partij uit.

Met batchverwerking kunt u instructies doorgeven voor verschillende bewerkingen in één HTTP-aanvraag. U kunt ook afhankelijkheden opgeven tussen verwante bewerkingen (zoals hieronder in een sectie wordt beschreven). TNT verwerkt elk van uw onafhankelijke bewerkingen (mogelijk parallel) en verwerkt uw afhankelijke bewerkingen opeenvolgend. Wanneer alle bewerkingen zijn voltooid, wordt een geconsolideerde reactie doorgegeven en wordt de HTTP-verbinding gesloten.

De batch-API neemt een array van logische HTTP-aanvragen op die als JSON-arrays worden vertegenwoordigd. Elke aanvraag heeft een methode (die overeenkomt met de HTTP-methode GET/PUT/POST/DELETE enz.), een relativeUrl (het gedeelte van de URL na admin/rest/), een optionele headerarray (die overeenkomt met HTTP-headers) en een optionele body (voor POST- en PUT-aanvragen). De batch-API retourneert een array met logische HTTP-reacties die worden vertegenwoordigd door JSON-arrays. Elke reactie heeft een statuscode, een optionele headerarray en een optionele body (die een JSON-gecodeerde tekenreeks is). Als u batchverzoeken wilt maken, maakt u een JSON-object dat elke afzonderlijke bewerking beschrijft die moet worden uitgevoerd. Het maximum aantal toegestane bewerkingen is 256 (van 0 tot 255).

Als u afhankelijkheden opgeeft tussen bewerkingen in de aanvraag Standaard zijn de bewerkingen die in de batch-API-aanvraag zijn opgegeven onafhankelijk. Deze kunnen in willekeurige volgorde op de server worden uitgevoerd en een fout in een bewerking heeft geen invloed op de uitvoering van andere bewerkingen.

Vaak zijn de bewerkingen in het verzoek afhankelijk. De uitvoer van een bewerking kan bijvoorbeeld worden gebruikt bij de invoer van de volgende bewerking. Bijvoorbeeld aanbieding die in operationId=0 wordt gecreeerd moet in campagnecreatie operationId=1 worden gebruikt.

Om twee batchbewerkingen aan elkaar te koppelen, geeft u in de afhankelijke bewerking de id van de vereiste bewerking op, bijvoorbeeld: &quot;hangtOnOperationId&quot; : 5. Ook kunnen id&#39;s van gemaakte bronnen via verzoeken van POSTEN van batchbewerkingen worden gebruikt in afhankelijke bewerkingen, zowel in &quot;relativeUrl&quot; als in &quot;body&quot;.

#### Machtigingen en rotatie

Voor het uitvoeren van batch-API-handelingen moet de onderliggende gebruiker ten minste ‘editor’-rechten hebben (voor elke afzonderlijke bewerking moeten aanvullende rechten worden vereist dan de gebruiker heeft, dan mislukt de afzonderlijke bewerking). De gebruikelijke vertragingsstrategieën worden toegepast op batch-API-acties alsof elke bewerking afzonderlijk is uitgevoerd.

De verwerking van de partij eindigt wanneer alle verrichtingen zijn voltooid, kon een verrichting of succesvol zijn (2xx statusCode), mislukking (4xx, 5xx statuscode) of overgeslagen omdat een gebiedsdeelverrichting is ontbroken of overgeslagen.

#### Objectparameters aanvragen

| Kenmerk | Beschrijving | Limieten | Standaard |
| --- | --- | --- | --- |
| lichaam | hoofdtekst voor HTTP-batchbewerking. wordt genegeerd voor alle acties, behalve voor POST en PUT. kan naar IDs van vorige partijacties verwijzen, bijvoorbeeld: &quot;aanbiedingId&quot;: &quot;{operationIdResponse:0}&quot;, &quot;segmentId&quot;: &quot;{operationIdResponse:1}&quot; | moet een geldige JSON zijn; in het geval dat naar een operationIdResponse verwijst, moet de operationID-respons een geldige ID zijn en moet de methode voor die actie POST zijn | leeg object {} |  |
| hangtOnOperationIds | lijst met beperkingen-id&#39;s die ervoor zorgen dat de huidige bewerking alleen wordt uitgevoerd als de opgegeven bewerkingen met succes zijn voltooid. Kan worden gebruikt om een keten van bewerkingen tot stand te brengen. | maximaal 255 bewerkingen zijn toegestaan; unieke waarden zijn alleen toegestaan; moeten verwijzen naar een geldige operationId in de array; cyclische afhankelijkheden zijn niet toegestaan |  |  |
| koppen | array van sleutelwaardeheaders die met bepaalde bewerking moeten worden verzonden. Als verificatie voor batch-API is uitgevoerd via de machtigingsheader, wordt deze ook gekopieerd voor afzonderlijke bewerkingen. | Het maximum aantal toegestane headers in de array is 50 | Inhoudstype: application/json |  |
| headers->name | koptekstnaam | moet uniek zijn onder andere koptekstnamen. De kopballen zijn geval ongevoelig door rfc, anders zullen de waarden elkaar met voeten treden. |  |  |
| headers->value | koptekstwaarde | NVT | lege tekenreeks |  |
| methode | Te gebruiken HTTP-methode. Beschikbare opties: GET, POST, PUT, PATCH, DELETE | alleen de methoden GET, POST, PUT, PATCH en DELETE zijn toegestaan |  |  |
| operationId | bewerking-id die wordt gebruikt om een bewerking te identificeren onder andere bewerkingen voor reacties en het verwijzen naar resultaten. | uniek onder andere verrichtingen; waarden van 0-255 |  |  |
| bewerkingen | lijst met bewerkingen die in een batch moeten worden uitgevoerd. orde is niet relevant. | maximaal 256 bewerkingen zijn toegestaan |  |  |
| relativeUrl | relatieve URL voor API voor rest van de beheerder, het onderdeel na &quot;/admin/rest/&quot;. Kan parameters voor queryreeksen bevatten, zoals: &quot;/v2/campagnes?limit=10&amp;offset=10&quot;. kan verwijzen naar URL&#39;s met id&#39;s van vorige batchhandelingen, bijvoorbeeld: &quot;/v1/aanbiedingen/{operationIdResponse:0}&quot;. Als queryparameters worden verzonden, moeten deze URL-gecodeerd zijn. | moet beginnen met / (relatief zijn); alleen nieuwe geldige JSON API&#39;s worden ondersteund; in geval van ongeldige relativeURL wordt een 404-reactie voor een bepaalde bewerking geretourneerd; in geval van verwijzing naar een operationIdResponse moet de operationId-respons een geldige id zijn en moet de methode voor die actie POST zijn |  |  |

#### Voorbeeld van aanvraagobject

```
{
  "operations": [
    {
      "operationId": 1,
      "dependsOnOperationIds~": [0],
      "method": "POST",
      "relativeUrl": "/v1/offers",
      "headers~": [
        {
          "name": "Content-Type",
          "value": "application/json"
        }
      ],
      "body~": {
        "key": "value"
      }
    }
  ]
}
```

#### Parameters van reactieobject

| Parameter | Beschrijving |
| --- | --- |
| operationId | bewerking-id die wordt gebruikt om een bewerking onder andere bewerkingen te identificeren, dezelfde id als die is verzonden in een verzoek om POST. |  |
| overgeslagen | markering boolen om te markeren of de bewerking is uitgevoerd of overgeslagen. Wordt true als de huidige bewerking afhankelijk is van een bewerking die is mislukt (een andere statusCode-waarde dan 2xx retourneert). |  |
| statusCode | geretourneerd, worden alle afhankelijke bewerkingen overgeslagen (niet uitgevoerd). |  |
| koppen | array van sleutelwaardeheaders die moeten worden verzonden als reactie op een bepaalde bewerking. |  |
| headers->name | koptekstnaam |  |
| headers->value | koptekstwaarde |  |
| lichaam | body for HTTP batch response operation |  |

#### Voorbeeld van reactieobject

```
{
  "results": [
    {
      "operationId": 1,
      "skipped~": false,
      "statusCode~": 200,
      "headers~": [
        {
          "name": "Content-Type",
          "value": "application/json; charset=UTF-8"
        }
      ],
      "body~": {
        "id": 5
      }
    }
  ]
}
```
