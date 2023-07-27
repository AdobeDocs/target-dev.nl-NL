---
title: De .NET SDK installeren
description: Leer hoe u de [!DNL Adobe Target] .NET SDK.
feature: APIs/SDKs
exl-id: 3cc84775-4692-4d14-9e82-db2873140835
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# De .NET SDK installeren

.NET SDK wordt verdeeld door [NuGet](https://www.nuget.org/packages/Adobe.Target.Client). Om te beginnen, voeg het als gebiedsdeel toe door via te installeren `Package Manage` of `.NET CLI`:

## Pakketbeheer

>[!BEGINTABS]

>[!TAB Pakketbeheer]

```csharp {line-numbers="true"}
Install-Package Adobe.Target.Client
```

>[!TAB .NET CLI]

```csharp {line-numbers="true"}
dotnet add package Adobe.Target.Client
```

>[!ENDTABS]

De open sourced code is te vinden op [https://github.com/adobe/target-dotnet-sdk](https://github.com/adobe/target-dotnet-sdk).
