---
title: Voer volmachtsconfiguratie in uit [!DNL Adobe Target] Node.js SDK
description: Leer hoe u de [!UICONTROL TargetClient] proxyconfiguratie in de [!DNL Adobe Target] Node.js SDK.
feature: APIs/SDKs
exl-id: c9f04e81-3fa3-4e64-a974-379420b0518a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Proxyconfiguratie (Node.js)

Om een volmacht voor de verzoeken van HTTP van de Knoop te vormen SDK, met voeten treedt halen API die door SDK tijdens initialisering wordt gebruikt.

Hier volgt een eenvoudig voorbeeld van hoe u het overschrijven kunt negeren `fetchApi` tijdens de `TargetClient` initialisatie om een proxy toe te voegen:

```javascript {line-numbers="true"}
const { ProxyAgent } = require("undici");

const proxyAgent = new ProxyAgent("your proxy address here");

const fetchImpl = (url, options) => {
  const fetchOptions = options;
  fetchOptions.dispatcher = proxyAgent;
  return fetch(url, fetchOptions);
};

client = TargetClient.create({
    ...,
    fetchApi: fetchImpl
});
```

Merk op dat dit slechts voor versies 18.2+ van de Knoop werkt, waarin `undici.fetch` is de standaardwaarde `fetch` voor knooppunt.
Ga naar [Node SDK samples repo](https://github.com/adobe/target-nodejs-sdk-samples/tree/master/proxy-configuration)
voor de voorbeelden van de volmachtsconfiguratie voor oudere versies van knoop en meer informatie.
