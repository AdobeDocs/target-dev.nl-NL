---
title: Abonneren aan gebeurtenissen in  [!DNL Adobe Target]  Python SDK
description: Leer hoe u zich abonneert op verschillende gebeurtenissen die plaatsvinden in de Python SDK met het [!UICONTROL OnDeviceDecisioningHandler] -object.
feature: APIs/SDKs
exl-id: 4e32e3b5-6072-4703-b09d-abb467aa1304
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# SDK Events (Python)

## Beschrijving

Wanneer [&#x200B; het initialiseren van SDK &#x200B;](initialize-sdk.md), is het `options["events"]` dict een facultatief voorwerp met de sleutels van de gebeurtenisnaam en callback functiewaarden. Deze kan worden gebruikt om een abonnement te nemen op verschillende gebeurtenissen die plaatsvinden in de SDK. De gebeurtenis `client_ready` kan bijvoorbeeld worden gebruikt met een callback-functie die wordt aangeroepen wanneer de SDK gereed is voor methodeaanroepen.

Wanneer de functie `callback` wordt aangeroepen, wordt een gebeurtenisobject doorgegeven. Elke gebeurtenis heeft een `type` die overeenkomt met de naam van de gebeurtenis. Sommige gebeurtenissen bevatten aanvullende eigenschappen met relevante informatie.

## Gebeurtenissen

| Naam gebeurtenis (type) | Beschrijving | Aanvullende gebeurteniseigenschappen |
| --- | --- | --- |
| client_ready | Geplaatst wanneer het artefact heeft gedownload en SDK klaar voor get_aanbiedingen vraag is. Aanbevolen bij gebruik van de beslissingsmethode op het apparaat. | Geen |
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
