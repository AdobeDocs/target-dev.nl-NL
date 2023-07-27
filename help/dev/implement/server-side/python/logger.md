---
title: Initialiseer de [!DNL Adobe Target] Python SDK om verzoeken te registreren
description: Leer hoe te om verzoeken in te loggen [!DNL Adobe Target] Python SDK.
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Logger (Python)

## Beschrijving

Wanneer [initialiseren SDK](initialize-sdk.md)de `options["logger"]` -object is een optioneel object. Standaard wordt een INFO-niveaunummer gemaakt onder de `adobe.target` naamruimte. Als u echter het logniveau wilt aanpassen of op effectieve wijze een foutopsporing wilt uitvoeren wanneer zich een probleem voordoet, wordt een `logger` -object kan worden opgegeven bij het initialiseren van de SDK.

De `logger` van het object wordt verwacht dat het een `debug()` en `error()` methode. Wanneer een geschikt registreerapparaat wordt geleverd, [!DNL Target] verzoeken en reacties worden geregistreerd.

## Voorbeeld

### Python

```python {line-numbers="true"}
logger = logging.getLogger("org.logger")
logger.setLevel(logging.DEBUG)

client_options = {
  "client": "acmeclient",
  "organization_id": "1234567890@AdobeOrg",
  "logger": logger
}
target_client = TargetClient.create(client_options)
```

U zou verzoeken en reacties moeten zien die in de console worden gedrukt.
