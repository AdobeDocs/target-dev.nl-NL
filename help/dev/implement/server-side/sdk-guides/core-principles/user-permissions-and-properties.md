---
title: Gebruikersmachtigingen en -eigenschappen
description: De [!DNL Target] SDK's bieden ondersteuning voor gebruikersmachtigingen en -eigenschappen.
exl-id: 612faf1a-e8f9-4321-b831-90fba69ead3a
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Gebruikersmachtigingen en -eigenschappen

De [!DNL Target] SDK&#39;s bieden ondersteuning voor gebruikersmachtigingen en -eigenschappen. Als u niet weet hoe [!DNL Adobe Target] behandelt ondernemingstoestemmingen via werkruimten en eigenschappen, kunt u meer over het in lezen [Machtigingen voor Enterprise-gebruikers](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=nl-NL).

De client kan op twee manieren een eigenschapstoken gebruiken.

## Token algemene eigenschap

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    propertyToken: "8c4630b1-16db-e2fc-3391-8b3d81436cfb"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({...})
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("emeaprod4")
    .organizationId("0DD934B85278256B0A490D44@AdobeOrg")
    .defaultPropertyToken("8c4630b1-16db-e2fc-3391-8b3d81436cfb")
    .build();

TargetClient targetClient = TargetClient.create(clientConfig);
```

>[!ENDTABS]

## Token van intrede van het Bezit in getOffers vraag

Een eigenschapstoken kan ook in een afzonderlijk bestand worden opgegeven `getOffers` vraag. Dit wordt gedaan door een bezitsobject aan het verzoek toe te voegen. Een bezitstoken op deze manier wordt gespecificeerd neemt precedent over één reeks in config die.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
    request: {
        execute: {
            pageLoad: {}
        },
        property: {
            token: "8c4630b1-16db-e2fc-3391-8b3d81436cfb"
        }           
    }
})
```

>[!TAB Java]

```java {line-numbers="true"}
ExecuteRequest executeRequest = new ExecuteRequest()
    .mboxes(getMboxRequests(mbox));

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
    .context(getContext(request))
    .execute(executeRequest)
    .cookies(getTargetCookies(request.getCookies()))
    .property(new Property().token("8c4630b1-16db-e2fc-3391-8b3d81436cfb"))
    .build();

TargetDeliveryResponse targetResponse = targetClient.getOffers(targetDeliveryRequest);
```

>[!ENDTABS]
