---
title: De Java SDK initialiseren met de methode create
description: Leer hoe u de methode create gebruikt om de Java SDK te initialiseren en het [!UICONTROL TargetClient] om vraag te maken aan [!DNL Adobe Target] voor experimenten en persoonlijke ervaringen.
feature: APIs/SDKs
exl-id: 0e0ddead-7de8-4549-b81c-e72598558e4b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 1%

---

# De SDK van Java initialiseren

## Beschrijving

Gebruik de `create` om de Java SDK te initialiseren en een instantie van de [!UICONTROL Target Client] om vraag te maken aan [!DNL Adobe Target] voor experimenten en persoonlijke ervaringen.

## Methode

[!UICONTROL TargetClient] wordt gemaakt met `TargetClient.create`.

### maken

```javascript {line-numbers="true"}
TargetClient TargetClient.create(ClientConfig clientConfig)
```

ClientConfig wordt gemaakt met `ClientConfig.builder`.

```javascript {line-numbers="true"}
ClientConfigBuilder ClientConfig.builder()
```

## Parameters

`ClientConfigBuilder` heeft de volgende structuur:

| Naam | Type | Vereist | Standaard | Beschrijving |
| --- | --- | --- | --- | --- |
| client | String | Ja | Geen | [!UICONTROL Target Client Id] |
| organisationId | String | Ja | Geen | [!UICONTROL Experience Cloud Organization ID] |
| connectTimeout | Getal | Nee | 10000 | Time-out voor verbinding voor alle aanvragen in milliseconden |
| socketTimeout | Getal | Nee | 10000 | Time-out van socket voor alle aanvragen in milliseconden |
| maxConnectionsPerHost | Getal | Nee | 100 | Max. verbindingen per [!DNL Target] host |
| maxConnectionsTotal | Getal | Nee | 200 | Max. verbindingen inclusief alle [!DNL Target] gastheren |
| enableRetries | Boolean | Nee | true | Automatisch opnieuw proberen voor sockettime-outs (max. 4) |
| logRequests | Boolean | Nee | false | Logboek [!DNL Target] verzoeken en reacties in foutopsporing |
| logRequestStatus | Boolean | Nee | false | Logboek [!DNL Target] reactietijd, status en URL |
| serverDomain | String | Nee | `*client*.tt.omtrdc.net` | Overschrijft de standaardhostnaam |
| beveiligen | Boolean | Nee | true | Ongedaan maken om HTTP-schema af te dwingen |
| requestInterceptor | HttpRequestInterceptor | Nee | Null | Aangepaste aanvraaginterceptor toevoegen |
| defaultPropertyToken | String | Nee | Geen | Hiermee wordt het standaard eigenschapstoken ingesteld voor elke `getOffers` vraag. **Voor het bepalen van het apparaat**, downloadt de SDK alleen het artefact dat de gekwalificeerde activiteiten bevat voor de eigenschap token die is ingesteld in `defaultPropertyToken` |
| defaultDecisioningMethod | DecisioningMethod enum | Nee | SERVER_SIDE | Moet worden ingesteld op ON_DEVICE of HYBRID om apparaatbeslissingen in te schakelen |
| telemetryEnabled | Boolean | Nee | true | Hiermee kunnen klanten weigeren extra gegevens te verzamelen tijdens aanvragen om [!DNL Target] servers |
| proxyConfig | ClientProxyConfig | Nee | Geen | Hiermee kan de client zijn eigen proxygegevens opgeven |
| exceptionHandler | TargetExceptionHandler | Nee | Geen | Kan worden gebruikt om de behandeling van de douaneuitzondering tijdens regelverwerking uit te voeren |
| httpClient | HttpClient | Nee | Geen | Hiermee kunnen gebruikers de [!DNL Target] HTTP-client met een aangepaste HTTP-client |
| onDeviceEnvironment | String | Nee | productie | Kan worden gebruikt om een andere apparaatomgeving op te geven, zoals ophaling |
| onDeviceConfigHostname | String | Nee | `assets.adobetarget.com` | Kan worden gebruikt om een andere host op te geven die moet worden gebruikt om het Artefactbestand voor beslissingen op het apparaat te downloaden |
| onDeviceDecisioningPollingIntSecs | int | Nee | 300 | Aantal seconden tussen terugwinning van het op apparaat beslissingsartefactdossier |
| onDeviceArtifactPayload | byte[] | Nee | Geen | Verstrekt op apparaat beslist met vorige artefactlading om directe uitvoering toe te staan |
| onDeviceDecisioningHandler | OnDeviceDecisioningHandler | Nee | Geen | Registreert callbacks voor op apparaat beslissingsgebeurtenissen |
| onDeviceAllMatchingRulesMboxes | Lijst\&lt;string> | Nee | Geen | Staat gebruikers toe om dozen te specificeren waarvoor alle passende regelinhoud tijdens op-apparatenbesluit zal zijn teruggekeerd |

## Voorbeeld

### Java

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient.create(clientConfig);

// make calls to Adobe Target
```
