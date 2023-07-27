---
title: De Python SDK initialiseren met de methode create
description: Leer hoe u de methode create gebruikt om de Python SDK te initialiseren en het [!UICONTROL TargetClient] om vraag te maken aan [!DNL Adobe Target] voor experimenten en persoonlijke ervaringen.
feature: APIs/SDKs
exl-id: 3e231e8e-696d-45c7-b733-79bf99da5bec
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# De Python SDK initialiseren

Beschrijving gebruiken `create` om de Python SDK te initialiseren en de [!UICONTROL Target Client] om vraag te maken aan [!DNL Adobe Target] voor experimenten en persoonlijke ervaringen.

## Methode

### maken

```python {line-numbers="true"}
TargetClient.create(options)
```

## Parameters

`options` heeft de volgende structuur:

| Naam | Type | Vereist | Standaard | Beschrijving |
| --- | --- | --- | --- | --- |
| client | str | Ja | Geen | [!UICONTROL Adobe Target client ID] |
| organisation_id | str | Ja | Geen | [!UICONTROL Experience Cloud Organization ID] |
| timeout | int | Nee | 3000 | Time-out in milliseconden |
| server_domain | str | Nee | `client.tt.omtrdc.net` |  | Overschrijft de standaardhostnaam |
| beveiligen | bool | Nee | true | Ongedaan maken om HTTP-schema af te dwingen |
| registreerapparaat | object | Nee | INFO-logboekregistratie |  | Hiermee vervangt u de standaard-INFO-logboekregistratie |
| target_location_hint | str | Nee | Geen | [!DNL Target] locatiehint |
| property_token | str | Nee | Geen | [!DNL Target] Token eigenschap. Als hier gespecificeerd, zullen alle get_aanbiedingen vraag deze waarde gebruiken. |
| beslissings_methode | str | Nee | server-kant | Bepaalt welke beslissingsmethode moet worden gebruikt ([op apparaat](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), server-kant, hybride) |
| polling_interval | int | Nee | 300000 (5 minuten) | Opiniepeilingsinterval voor de [Artefact van regel voor apparaatbeslissingen](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) (in ms) |
| artefact_location | str | Nee | Geen | Een volledig gekwalificeerde URL naar de [Artefact van regel voor apparaatbeslissingen](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Hiermee overschrijft u de intern bepaalde locatie. |
| artifact_payload | object | Nee | Geen | De JSON-lading van de [Artefact van regel voor apparaatbeslissingen](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Indien opgegeven, wordt deze gebruikt in plaats van een aanvraag via een URL in te dienen. |
| [gebeurtenissen](sdk-events.md) | dict &lt;str callable=&quot;&quot;> | Nee | Geen | Een optioneel object met gebeurtenisnaamtoetsen en callback-functiewaarden |
| environment_id | int | Nee | productie | De [!DNL Target] milieu-id |
| milieu | str | Nee | productie | De [!DNL Target] omgevingsnaam |
| cdn_environment | str | Nee | productie | De CDN-omgevingsnaam |
| telemetrie_enabled | bool | Nee | Waar | Indien ingesteld op False, worden telemetriegegevens niet verzonden naar [!DNL Adobe] |
| versie | str | Nee | Geen | Het versienummer van deze SDK |

## Voorbeeld

### Python

```python {line-numbers="true"}
from target_python_sdk import TargetClient

def client_ready_callback(ready_event):
    # make calls to Adobe Target

client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
