---
title: Voer volmachtsconfiguratie in uit [!DNL Adobe Target] Java SDK
description: Leer hoe te om de volmachtsconfiguratie te vormen TargetClient in [!DNL Adobe Target] Java SDK.
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
source-git-commit: 59ab3f53e2efcbb9f7b1b2073060bbd6a173e380
workflow-type: tm+mt
source-wordcount: '170'
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

## Apparaatbeslissingen

Voor verzoeken om het regelartefact te halen, zou uw volmacht moeten worden gevormd om de reactie niet in het voorgeheugen onder te brengen. Nochtans, als het niet mogelijk is om het caching mechanisme van de volmacht voor dat verzoek te vormen, gebruik een configuratieoptie als oplossing om het volmacht-vlakke geheime voorgeheugen te mijden. Deze tijdelijke oplossing voegt de `Authorization` header met een lege tekenreekswaarde op de regelingenaanvraag, die aan de proxy moet aangeven dat de reactie niet in de cache moet worden opgeslagen.

Stel het volgende in om deze tijdelijke oplossing in te schakelen:

```java {line-numbers="true"}
ClientConfig.builder()
    .shouldArtifactRequestBypassProxyCache(true)
    .build();
```


