---
title: Initialiseer .NET SDK gebruikend creeer methode
description: Leer hoe u de methode create gebruikt om de Java SDK te initialiseren en het [!UICONTROL TargetClient] om vraag te maken aan [!DNL Adobe Target] voor experimenten en persoonlijke ervaringen.
feature: APIs/SDKs
exl-id: 501010c3-22f4-49a8-b2ac-c7307232d180
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Initialiseer .NET SDK

## Beschrijving

Gebruik de `Create` om .NET SDK te initialiseren en het [!UICONTROL Target Client] om vraag te maken aan [!DNL Adobe Target] voor experimenten en persoonlijke ervaringen.

Wanneer het gebruiken van .NET Injectie van de Afhankelijkheid, voeg enkel SDK bij de stap van de de dienstconfiguratie toe door te roepen `services.AddTargetLibrary()`; injecteren `ITargetClient targetClient` in de constructor van uw app.

Gebruik daarna de `Initialize` methode van SDK om SDK te vormen, waarbij de initialisatiestap wordt voltooid.

## Methode

`TargetClient` wordt gemaakt met `TargetClient.Create`.

## C\
#

```csharp {line-numbers="true"}
TargetClient TargetClient.Create(TargetClientConfig clientConfig)
```

`ClientConfig` wordt gecreeerd gebruikend ClientConfig.Builder.

## C\
#

```csharp {line-numbers="true"}
TargetClientConfig.Builder TargetClientConfig.Builder()
```

## Parameters

`TargetClientConfig.Builder` heeft de volgende structuur:

| Naam | Type | Vereist | Standaard | Beschrijving |
| --- | --- | --- | --- | --- |
| Client | string | Ja | Geen | [!UICONTROL Target Client Id] |
| Organisatie-id | string | Ja | Geen | [!UICONTROL Experience Cloud Organization ID] |
| Time-out | int | Nee | 10000 | Time-out voor alle aanvragen in milliseconden |
| Proxy |  | WebProxy | Nee | null | Proxy voor alles [!DNL Target] verzoeken |
| OpnieuwPolicy | Beleid | Nee | null | Beleid voor iedereen opnieuw proberen [!DNL Target] verzoeken |
| AsyncRetryPolicy | AsyncPolicy | Nee | null | Beleid voor opnieuw proberen synchroniseren voor iedereen [!DNL Target] verzoeken |
| Aanmelder | ILogger | Nee | null | Wordt gebruikt voor foutopsporingslogboekregistratie van [!DNL Target] verzoeken en antwoorden |
| ServerDomain | string | Nee | `client.tt.omtrdc.net` | Overschrijft de standaardhostnaam |
| Beveiligen | bool | Nee | true | Ongedaan maken om HTTP-schema af te dwingen |
| DefaultPropertyToken | string | Nee | null | Hiermee wordt het standaard eigenschapstoken ingesteld voor elke `getOffers` call |
| TelemetryEnabled | bool | Nee | true | Telemetriegegevens verzenden om het gebruik van SDK te verbeteren |
| DecisioningMethod | DecisioningMethod enum | Nee | ServerSide | Moet worden ingesteld op OnDevice of Hybrid om apparaatbeslissingen mogelijk te maken |
| OnDeviceDecisioningReady | Handeling | Nee | null | Delegeren voor de gebeurtenis Klaar voor beslissingen op het apparaat (één keer opgeroepen wanneer de beslissing op het apparaat gereed is) |
| ArtifactDownloadSuccceeded | Handeling | Nee | null | Delegeren voor het downloaden van artefacten voor beslissingen op het apparaat (aangeroepen voor elke geslaagde artefactdownload) |
| ArtifactDownloadFailed | Handeling | Nee | null | Delegeren voor downloadfout van beslissingsartefact op apparaat (aangeroepen voor elke mislukte artefactdownload) |
| OnDeviceEnvironment | string | Nee | productie | Kan worden gebruikt om een andere apparaatomgeving op te geven, zoals ophaling |
| OnDeviceConfigHostname | string | Nee | `assets.adobetarget.com` | Kan worden gebruikt om een andere host op te geven die moet worden gebruikt om het Artefactbestand voor beslissingen op het apparaat te downloaden |
| OnDeviceDecisioningPollingIntSecs | int | Nee | 300 (5 min) | Aantal seconden tussen terugwinning van het op apparaat beslissingsartefactdossier |
| OnDeviceArtifactPayload | string | Nee | null | Verstrekt op apparaat beslist met een lokale artefactlading om directe uitvoering toe te staan |

## Voorbeeld

## C\
#

```csharp {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeclient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

targetClient = TargetClient.Create(targetClientConfig);

// make calls to Adobe Target
```
