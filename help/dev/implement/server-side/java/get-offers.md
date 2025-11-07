---
title: Gebruik getOffers () in  [!DNL Adobe Target]  wanneer het gebruiken van Java SDK
description: Leer hoe te om getOffers () te gebruiken om een besluit uit te voeren en een ervaring van terug te winnen  [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 9d7bf956-9d6a-4b4f-a401-2e6814f17f3d
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Voorstel ophalen (Java)

## Beschrijving

`getOffers()` wordt gebruikt om een beslissing uit te voeren en een ervaring op te halen uit [!DNL Adobe Target] .

## Methode

### getOffers

De handtekening van de methode `TargetClient.getOffers` wordt als volgt weergegeven.

**Verzoek**

```javascript {line-numbers="true"}
TargetDeliveryResponse TargetClient.getOffers(TargetDeliveryRequest request)
```

TargetDeliveryRequest wordt gemaakt met `TargetDeliveryRequest.builder`.

**Reactie**

```javascript {line-numbers="true"}
TargetDeliveryRequestBuilder TargetDeliveryRequest.builder()
```

## Parameters

Het `[!UICONTROL TargetDeliveryRequestBuilder]` -object heeft de volgende structuur:

| Naam | Type | Vereist | Beschrijving |
| --- | --- | --- | --- |
| context | Context | Ja | Geeft de context voor de aanvraag op |
| sessionId | String | Nee | Wordt gebruikt voor het koppelen van meerdere [!DNL Target] -aanvragen |
| thirdPartyId | String | Nee | Uw bedrijfs herkenningsteken voor de gebruiker die u met elke vraag kunt verzenden |
| cookies | Lijst | Nee | Lijst met cookies die zijn geretourneerd in vorige [!DNL Target] aanvraag van dezelfde gebruiker. |
| customerIds | Kaart | Nee | Klant-id&#39;s in de indeling VisitorId die compatibel is met |
| uitvoeren | ExecuteRequest | Nee | PageLoad of vakjes verzoeken uit te voeren. Wordt meteen aan de serverzijde geëvalueerd |
| prefetch | PrefetchRequest | Nee | Weergaven, PageLoad of vakjes vragen om een voorvoegsel. Retourneert met berichttoken dat moet worden geretourneerd bij conversie. |
| meldingen | Lijst | Nee | Gebruikt om meldingen te verzenden over welke vooraf ingestelde inhoud werd weergegeven |
| requestId | String | Nee | De aanvraag-id die in de reactie wordt geretourneerd. Automatisch gegenereerd als dit niet het geval is. |
| pictureId | String | Nee | Indien aanwezig, zullen de tweede en verdere verzoeken met zelfde identiteitskaart geen impressies aan activiteiten/metriek verhogen. Automatisch gegenereerd als dit niet het geval is. |
| environmentId | Lang | Nee | Geldige client environment-id. Indien niet opgegeven host wordt bepaald op basis van de opgegeven host. |
| eigenschap | Eigenschap | Nee | Specifies the at_property via the token field. Het kan worden gebruikt om de draagwijdte voor de levering te controleren. |
| traceren | Traceren | Nee | Schakelt tracering voor levering-API in. |
| qaMode | QAMode | Nee | Gebruik dit object om de QA-modus in de aanvraag in te schakelen. |
| locationHint | String | Nee | [!DNL Target] Locatiehint randcluster. Wordt gebruikt om opgegeven Edge-clusters voor deze aanvraag als doel in te stellen. |
| bezoeker | Bezoeker | Nee | Wordt gebruikt om een aangepast Bezoeker-API-object aan te bieden. |
| id | VisitorId | Nee | Object dat de id&#39;s voor de bezoeker bevat. Eg. tntId, thirdParyId, mcId, customerIds. |
| ExperienceCloud | ExperienceCloud | Nee | Geeft integratie met Audience Manager en Analytics aan. Automatisch vullen met behulp van cookies, indien niet beschikbaar. |
| tntId | String | Nee | Primaire id in [!DNL Target] voor een gebruiker. Vanuit targetCookies gevonden. Automatisch gegenereerd als dit niet is opgegeven. |
| mcId | String | Nee | Wordt gebruikt om gegevens samen te voegen en te delen tussen verschillende [!DNL Adobe] -oplossingen (ECID). Vanuit targetCookies gevonden. Automatisch gegenereerd als dit niet is opgegeven. |
| trackingServer | String | Nee | De Adobe Analytics-server zodat [!DNL Adobe Target] en [!DNL Adobe Analytics] de gegevens op de juiste wijze aan elkaar kunnen koppelen. |
| trackingServerSecure | String | Nee | De lus [!UICONTROL Adobe Analytics Secure Server] zodat [!DNL Adobe Target] en [!DNL Adobe Analytics] de gegevens op de juiste wijze aan elkaar kunnen koppelen. |
| determinoningMethod | DecisioningMethod | Nee | Kan worden gebruikt om de ON_DEVICE- of HYBRID-beslissingsmethode expliciet in te stellen voor apparaatbeslissingen |

De waarden van elk veld moeten voldoen aan de aanvraagspecificatie van *[!UICONTROL Target View Delivery API]* . Meer over *[!UICONTROL Target View Delivery API]* leren, zie [ http://developers.adobetarget.com/api/#view-delivery-overview ](http://developers.adobetarget.com/api/#view-delivery-overview)


## Antwoord

De `TargetDeliveryResponse` die door `TargetClient.getOffers(` wordt geretourneerd) heeft de volgende structuur:

| Naam | Type | Beschrijving |
| --- | --- | --- |
| verzoek | TargetDeliveryRequest-&#x200B; | *[!DNL Target]* request |
| reactie | DeliveryResponse | *[!DNL Target]* reactie |
| cookies | Lijst | Lijst met sessiemetagegevens voor deze gebruiker. Moet worden overgegaan in volgende doelverzoek voor deze gebruiker. |
| bezoekerState | Kaart | Bezoekersstatus op de client in te stellen voor gebruik door de Bezoeker-API |
| responseStatus | ResponseStatus | Een object dat de status van het antwoord vertegenwoordigt |

De `ResponseStatus` in het antwoord bevat de volgende velden:

| Naam | Type | Beschrijving |
| --- | --- | --- |
| status | int | HTTP-status geretourneerd van [!DNL Target] |
| message | String | Statusbericht als de HTTP-status niet 200 is |
| remoteMboxes | Lijst met tekenreeksen | Wordt gebruikt voor apparaatbeslissingen. Bevat een lijst van dozen die verre activiteiten hebben die niet volledig op-apparaat kunnen worden beslist. |
| remoteViews | Lijst met tekenreeksen | Wordt gebruikt voor apparaatbeslissingen. Bevat een lijst van meningen die verre activiteiten hebben die niet volledig op-apparaat kunnen worden beslist. |

Het `TargetCookie` -object dat wordt gebruikt voor het opslaan van gegevens voor een gebruikerssessie, heeft de volgende structuur:

| Naam | Type | Beschrijving |
| --- | --- | --- |
| name | String | Naam cookie |
| value | String | Cookie-waarde, de waarde wordt omgezet in tekenreeks |
| maxAge | Getal | De optie maxAge is een handigheid voor het instellen van een vervaldatum ten opzichte van de huidige tijd in seconden |

Je hoeft je geen zorgen te maken over het verlopen van de cookies. Het doel handelt maxAge binnen de SDK af.

## Voorbeeld

**Verzoek**

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);

List<MboxRequest> mboxRequests = new ArrayList<>();
mboxRequests.add((MboxRequest) new MboxRequest().name("a1-serverside-ab").index(1));

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .execute(new ExecuteRequest().setMboxes(mboxRequests))
        .build();
```

**Reactie**

```javascript {line-numbers="true"}
TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
```
