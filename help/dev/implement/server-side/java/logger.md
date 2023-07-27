---
title: Initialiseer de [!DNL Adobe Target] Java SDK om aanvragen te registreren
description: Leer hoe te om verzoeken in te loggen [!DNL Adobe Target] Java SDK.
feature: APIs/SDKs
exl-id: 85d1a6ef-0b08-4948-8133-740b7d6141dd
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# Aanmelder (Java)

## Beschrijving

Wanneer [initialiseren SDK](initialize-sdk.md)Er zijn verschillende opties voor de `ClientConfig` -object, dat kan worden ingesteld op logverzoeken.

| Optie | Beschrijving |
| --- | --- |
| `logRequests` | Logs gehele verzoeklichaam evenals reactielichaam. |
| `logRequestStatus` | De URL van het verzoek van logs, status samen met reactietijd. |

[!DNL Target] Java SDK gebruikt `slf4j` registreren. U moet uw implementatie van registreerapparaat zoals verstrekken `java.util.logging`, `logback`, en `log4j`. Zie [http://www.slf4j.org/manual.html](http://www.slf4j.org/manual.html) voor meer informatie . Alle logbestanden worden afgedrukt in `debug`.

## Voorbeeld

Voeg de `slf4j` afhankelijkheid.

>[!BEGINTABS]

>[!TAB Gradient]

### Gradient

```javascript {line-numbers="true"}
compile 'org.slf4j:slf4j-simple:2.0.0-alpha0'
```

>[!TAB Maven]

```javascript {line-numbers="true"}
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-simple</artifactId>
    <version>2.0.0-alpha0</version>
</dependency>
```

>[!ENDTABS]

De optie `DEBUG` logboeken die op uw implementatie worden gebaseerd, en merken de vlaggen van het verzoekregistreren.

### Foutopsporing

```javascript {line-numbers="true"}
System.setProperty(SimpleLogger.DEFAULT_LOG_LEVEL_KEY, "DEBUG");
ClientConfig config = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .logRequests(true)
        .logRequestStatus(true)
        .build();

TargetClient targetClient = TargetClient.create(config);
```

U zou verzoeken, reacties, en reactietijden moeten zien die in de console worden gedrukt.
