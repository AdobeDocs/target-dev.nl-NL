---
title: getOffers() gebruiken in [!DNL Adobe Target] wanneer het gebruiken van .NET SDK
description: Leer hoe u getOffers() gebruikt om een beslissing uit te voeren en een ervaring op te halen uit [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 4d1d1cbd-c7e5-4146-9fea-08e01923874d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Aanbiedingen ophalen (.NET)

## Beschrijving

`GetOffers()` wordt gebruikt om een besluit uit te voeren en een ervaring van terug te winnen [!DNL Adobe Target].

## Methode

`TargetClient.GetOffers` methodehandtekening.

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.GetOffers(TargetDeliveryRequest request)
```

`TargetDeliveryRequest` wordt gemaakt met `TargetDeliveryRequest.Builder`.

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryRequest.Builder TargetDeliveryRequest.Builder()
```

## Parameters

De `TargetDeliveryRequest.Builder` object heeft de volgende structuur:

| Naam | Type | Vereist | Beschrijving |
| --- | --- | --- | --- |
| context | Context | Ja | Geeft de context voor de aanvraag op |
| sessionId | String | Nee | Wordt gebruikt voor het koppelen van meerdere [!DNL Target] verzoeken |
| thirdPartyId | String | Nee | Uw bedrijfs herkenningsteken voor de gebruiker die u met elke vraag kunt verzenden |
| cookies | Lijst | Nee | Lijst met cookies die zijn geretourneerd in vorige [!DNL Target] verzoek van dezelfde gebruiker. |
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
| locationHint | String | Nee | [!DNL Target] locatiehint randcluster. Wordt gebruikt om opgegeven Edge-clusters voor deze aanvraag als doel in te stellen. |
| bezoeker | Bezoeker | Nee | Wordt gebruikt om een aangepast Bezoeker-API-object aan te bieden. |
| id | VisitorId | Nee | Object dat de id&#39;s voor de bezoeker bevat. Eg. tntId, thirdParyId, mcId, customerIds. |
| ExperienceCloud | ExperienceCloud | Nee | Geeft integratie met Audience Manager en Analytics aan. Automatisch vullen met behulp van cookies, indien niet beschikbaar. |
| tntId | String | Nee | Primaire id in [!DNL Target] voor een gebruiker. Vanuit targetCookies gevonden. Automatisch gegenereerd als dit niet is opgegeven. |
| mcId | String | Nee | Wordt gebruikt om gegevens tussen verschillende Adobe-oplossingen (ECID) samen te voegen en te delen. Vanuit targetCookies gevonden. Automatisch gegenereerd als dit niet is opgegeven. |
| trackingServer | String | Nee | De Adobe Analytics-server [!DNL Adobe Target] en [!DNL Adobe Analytics] om de gegevens correct aan elkaar te koppelen. |
| trackingServerSecure | String | Nee | De [!UICONTROL Adobe Analytics Secure Server] om [!DNL Adobe Target] en [!DNL Adobe Analytics] om de gegevens correct aan elkaar te koppelen. |
| determinoningMethod | DecisioningMethod | Nee | Kan worden gebruikt om de ON_DEVICE- of HYBRID-beslissingsmethode expliciet in te stellen voor apparaatbeslissingen |

De waarden van elk veld moeten overeenkomen met [API voor doellevering](/help/dev/implement/delivery-api/overview.md) verzoek specificeren.

## Antwoord

De `TargetDeliveryResponse` geretourneerd door `TargetClient.GetOffers()` heeft de volgende structuur:

| Naam | Type | Beschrijving |
| --- | --- | --- |
| Verzoek | TargetDeliveryRequest-&#x200B; | [API voor doellevering](/help/dev/implement/delivery-api/overview.md) verzoek |
| Antwoord | &#x200B; | [API voor doellevering](/help/dev/implement/delivery-api/overview.md)* reactie |
| Status | HttpStatusCode | HTTP-statuscode van response |
| Bericht | string | Bericht met status van reactie of foutbericht |
| Locaties | Locaties | [!DNL Target] locatienamen, inclusief algemene naam van de box en vakken/weergaven waarvoor alleen externe beslissingen beschikbaar zijn |
| GetCookies | Woordenboek | Retourneert een woordenboek met sessiemetagegevens voor deze gebruiker. Dit moet in de volgende [!DNL Target] aanvraag voor deze gebruiker. |
| VisitorState | IDictionary | Bezoekerstatus aan clientzijde voor Javascript-bibliotheekinitialisatie voor bezoeker-API |

De `TargetCookie` Het object dat wordt gebruikt voor het opslaan van gegevens voor gebruikerssessie heeft de volgende structuur:

| Naam | Type | Beschrijving |
| --- | --- | --- |
| Naam | string | Naam cookie |
| Waarde | string | Cookie-waarde |
| MaxAge | int | De `MaxAge` is een handige optie voor het instellen van Verlopen in verhouding tot de huidige tijd in seconden |

Je hoeft je geen zorgen te maken over het verlopen van de cookies. [!DNL Target] handgrepen `MaxAge` in de SDK.

## Voorbeeld

## \.NET

```dotnet {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

var targetClient = TargetClient.Create(targetClientConfig);

var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .SetExecute(new ExecuteRequest(mboxes: mboxRequests))
    .Build();

var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
```
