---
title: Initialiseer  [!DNL Adobe Target]  Java SDK om verzoeken te registreren
description: Leer hoe te om verzoeken in  [!DNL Adobe Target]  Java SDK te registreren.
feature: APIs/SDKs
exl-id: 85d1a6ef-0b08-4948-8133-740b7d6141dd
source-git-commit: 526445fccee9b778b7ac0d7245338f235f11d333
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Aanmelder (Java)

## Beschrijving

Wanneer [ het initialiseren van SDK ](initialize-sdk.md), zijn er verscheidene opties op het `ClientConfig` voorwerp, dat aan logboekverzoeken kan worden geplaatst.

| Optie | Beschrijving |
| --- | --- |
| `logRequests` | Logs gehele verzoeklichaam evenals reactielichaam. |
| `logRequestStatus` | De URL van het verzoek van logs, status samen met reactietijd. |

[!DNL Target] Java SDK gebruikt `slf4j` -logboekregistratie. U moet uw implementatie van registreerapparaten zoals `java.util.logging`, `logback`, en `log4j` verstrekken. Verwijs naar [ https://www.slf4j.org/manual.html ](https://www.slf4j.org/manual.html) voor meer informatie. Alle logbestanden worden afgedrukt in `debug` .

## Voorbeeld

Voeg de `slf4j` afhankelijkheid toe.

>[!BEGINTABS]

>[!TAB  Gradle ]

### Gradient

```javascript {line-numbers="true"}
compile 'org.slf4j:slf4j-simple:2.0.0-alpha0'
```

>[!TAB  Gemaakt ]

```javascript {line-numbers="true"}
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-simple</artifactId>
    <version>2.0.0-alpha0</version>
</dependency>
```

>[!ENDTABS]

Schakel de `DEBUG` -logboeken in op basis van uw implementatie en markeer de aanvraaglogboekmarkeringen.

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
