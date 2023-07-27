---
title: Initialiseer de [!DNL Adobe Target] Node.js SDK aan logboekverzoeken
description: Leer hoe te om verzoeken in te loggen [!DNL Adobe Target] Node.js SDK.
feature: APIs/SDKs
exl-id: 5db3e301-47b3-4330-b185-c0c03f72e790
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---

# Logger (Node.js)

## Beschrijving

Wanneer [initialiseren SDK](initialize-sdk.md)de `options.logger` -object is een optioneel object. Als u echter effectief wilt foutopsporing wanneer een probleem optreedt, moet u `logger` moet een object worden opgegeven bij het initialiseren van de SDK.

De `logger` van het object wordt verwacht dat het een `debug()` en `error()` methode. Wanneer een geschikt registreerapparaat wordt verstrekt, zoals `console`, [!DNL Target] verzoeken en reacties worden geregistreerd.

## Voorbeeld

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  logger: console
};

const targetClient = TargetClient.create(CONFIG);

const request = {
    execute: {
        mboxes: [{
            name: "a1-serverside-ab",
            index: 1
        }]
    }
};

const response = await targetClient.getOffers({ request, targetCookie });
```

U zou verzoeken en reacties moeten zien die in de console worden gedrukt.
