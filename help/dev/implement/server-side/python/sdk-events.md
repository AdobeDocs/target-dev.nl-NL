---
title: Abonneren op gebeurtenissen in het dialoogvenster [!DNL Adobe Target] Python SDK
description: Leer hoe u zich kunt abonneren op verschillende gebeurtenissen die plaatsvinden in de Python SDK met de [!UICONTROL OnDeviceDecisioningHandler] object.
feature: APIs/SDKs
exl-id: 4e32e3b5-6072-4703-b09d-abb467aa1304
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# SDK-gebeurtenissen (Python)

## Beschrijving

Wanneer [initialiseren SDK](initialize-sdk.md)de `options["events"]` dict is een optioneel object met gebeurtenisnaamtoetsen en callback-functiewaarden. Het kan worden gebruikt om aan diverse gebeurtenissen in te tekenen die binnen SDK voorkomen. Bijvoorbeeld de `client_ready` De gebeurtenis kan met een callback functie worden gebruikt die zal worden aangehaald wanneer SDK klaar voor methodevraag is.

Wanneer de `callback` wordt aangeroepen, wordt een gebeurtenisobject doorgegeven. Elke gebeurtenis heeft een `type` komt overeen met de naam van de gebeurtenis en sommige gebeurtenissen bevatten aanvullende eigenschappen met relevante informatie.

## Gebeurtenissen

| Naam gebeurtenis (type) | Beschrijving | Aanvullende gebeurteniseigenschappen |
| --- | --- | --- |
| client_ready | Geplaatst wanneer het artefact heeft gedownload en SDK klaar voor get_aanbiedingen vraag is. Aanbevolen bij gebruik | op het apparaat beslissingsmethode. | Geen |
| artifact_download_managed | Wordt telkens verzonden wanneer een nieuw artefact wordt gedownload. | artefact_payload, artefact_location |
| artefact_download_failed | Wordt telkens verzonden wanneer een artefact niet kan worden gedownload. | artefact_location, fout |

## Voorbeeld

### Python

```python {line-numbers="true"}
def client_ready_callback():
    # make get_offers requests

def artifact_download_succeeded(event):
    print("The artifact was successfully downloaded from {}".format(event.artifact_location))
    # optionally do something with event.artifact_payload, like persist it

def artifact_download_failed(event):
    print("The artifact failed to download from {} with the following error: {}"
          .format(event.artifact_location, str(event.error)))

client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback,
        "artifact_download_succeeded": artifact_download_succeeded,
        "artifact_download_failed": artifact_download_failed
    }
}
target_client = target_client.create(client_options)
```
