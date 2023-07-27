---
title: Leer hoe u de aangepaste HTTP-client configureert
description: Leer hoe u TargetClient configureert met ClientConfig.builder().httpClient().
feature: APIs/SDKs
exl-id: 7615029c-b62d-4ed1-aadb-32e364c4c654
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Aangepaste HTTP Client Configuration (Java)

Als de toepassing die de SDK uitvoert een aangepaste HTTP-client nodig heeft om functies in te schakelen zoals SSL configureren of standaardheaders aan aanvragen toevoegen, `TargetClient` zal moeten worden gevormd gebruikend `ClientConfig.builder().httpClient()`:

## Standaard aangepaste HTTP-clientconfiguratie

De SDK biedt momenteel ondersteuning voor HTTP-clients die de `org.apache.http.client.HttpClient` interface.

### Basisimplementatie

```java {line-numbers="true"}
CloseableHttpClient httpClient = HttpClients.custom().build();
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .httpClient(httpClient)
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Aangepaste HTTP-clientconfiguratie met SSL-configuratie

Hier is een voorbeeld van hoe te om SSL in te vormen `TargetClient` door de `HttpClient` worden doorgegeven aan de `ClientConfig`. Het volgende codefragment gebruikt klassen uit het `org.apache.http.conn.ssl` pakket voor SSL-configuratie.

### SSL-implementatie

```java {line-numbers="true"}
SSLContext context = SSLContextBuilder.create().build();
SSLConnectionSocketFactory sslSocketFactory = new SSLConnectionSocketFactory(context);
CloseableHttpClient httpClient = HttpClients.custom().setSSLSocketFactory(sslSocketFactory).build();
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .httpClient(httpClient)
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```
