---
title: Voer volmachtsconfiguratie in uit [!DNL Adobe Target] Java SDK
description: Leer hoe te om de volmachtsconfiguratie te vormen TargetClient in [!DNL Adobe Target] Java SDK.
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Proxyconfiguratie (Java)

## Standaardproxy

Als de toepassing die de SDK uitvoert, een proxy nodig heeft voor toegang tot internet, `TargetClient` zal met een volmachtsconfiguratie als volgt moeten worden gevormd.

### Standaardproxyconfiguratie

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Verificatie

Als een volmachtsauthentificatie wordt vereist, kunnen de geloofsbrieven als parameters tot worden overgegaan `ClientProxyConfig` constructor, zoals in het onderstaande voorbeeld. Merk op dat dit slechts voor eenvoudige gebruikersbenaming/wachtwoordvolmachtsauthentificatie werkt.

### Standaardproxyverificatie

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port,username,password))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```
