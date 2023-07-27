---
title: De SDK van Java installeren
description: Leer hoe u de [!DNL Adobe Target] Java SDK.
feature: APIs/SDKs
exl-id: 5828d5b3-c487-49bf-9458-7ef94374e32d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# De SDK van Java installeren

De Java SDK wordt gedistribueerd door [Maven Central](https://search.maven.org/artifact/com.adobe.target/target-java-sdk). Om te beginnen, voeg het als gebiedsdeel toe door binnen te installeren `gradle` of `maven`:

>[!BEGINTABS]

>[!TAB Gradient]

```javascript {line-numbers="true"}
compile 'com.adobe.target:java-sdk:1.0'
```

>[!TAB Maven]

```javascript {line-numbers="true"}
<dependency>
    <groupId>com.adobe.target</groupId>
    <artifactId>java-sdk</artifactId>
    <version>2.0</version>
</dependency>
```

>[!ENDTABS]

De open sourced code is te vinden op <https://github.com/adobe/target-java-sdk>.
