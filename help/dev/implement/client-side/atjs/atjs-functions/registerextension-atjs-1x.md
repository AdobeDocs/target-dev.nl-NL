---
keywords: registerExtension, registerextensie, registerextensie, at.js, functies, functie, clientCode, serverDomain, globalMboxName, globalMboxAutoCreate, timeout, registerExtension2
description: Gebruik de [!UICONTROL registerExtension()] functie voor de [!DNL Adobe Target] at.js JavaScript-bibliotheek om een specifieke extensie te registreren. (om 1.js)
title: Hoe gebruik ik de [!UICONTROL registerExtension()] Functie?
feature: at.js
exl-id: 71decf00-84c5-4914-b0cd-bb061fa6265f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 1%

---

# [!UICONTROL registerExtension()] - om.js 1.x

Verstrekt een standaardmanier om een specifieke uitbreiding te registreren.

>[!NOTE]
>
>Deze functie is beschikbaar voor at.js versies 1.*x* alleen. Deze functie is vervangen door de release van at.js 2.*x*. Deze functie retourneert standaardinhoud als deze wordt gebruikt met at.js 2.x.

De parameter options is verplicht en heeft de volgende structuur:

| Sleutel | Type | Vereist | Beschrijving |
|--- |--- |--- |--- |
| name | String | Ja | Naam van extensie. |
| modules | Array[String] | Ja | Een array van tekenreeksen die opgevraagde modulenamen vertegenwoordigen. |
| registreren | -functie | Ja | Een functie die wordt gebruikt om de extensie te initialiseren en samen te stellen. Deze functie ontvangt argumenten die op modules serie worden gebaseerd. |

Opmerkingen:

* Als een van de parameters niet wordt opgegeven, wordt een uitzondering gegenereerd.
* Als de array modules leeg is, wordt een uitzondering gegenereerd.

Voor meer informatie en voorbeelden van hoe te gebruiken `[!UICONTROL registerExtension]`, zie de [Adobe Experience Cloud Target-objectextensies](https://github.com/Adobe-Marketing-Cloud/target-atjs-extensions) pagina op GitHub.

## Methoden van de module Instellingen

| Sleutel | Type | Beschrijving |
|--- |--- |--- |
| clientCode | String | Clientcode |
| serverDomain | String | Edge-serverdomein |
| globalMboxName | String | [!DNL Target] algemene naam van de box |
| globalMboxAutoCreate | Boolean | Geeft aan of automatisch maken is ingeschakeld |
| timeout | Getal | Verzoek om time-out |

## Methoden van de module Logger

| Sleutel | Type | Beschrijving |
|--- |--- |--- |
| log | -functie | Logs de veranderlijke lijst van argumenten aan de browser console, als het bestaat. Het wordt alleen geactiveerd wanneer `mboxDebug=true` wordt doorgegeven aan de URL. |
| fout | -functie | Logs de veranderlijke lijst van argumenten aan de browser console. Het wordt geactiveerd slechts wanneer er ernstige fouten zijn, zoals netwerkonderbreking, HTML knoop niet gevonden, enz. |
