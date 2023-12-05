---
title: Adobe Target Profiles-API
description: Leer hoe u API's met Adobe Target-profielen kunt gebruiken om bezoekersgegevens te verzenden naar [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
source-git-commit: e5a1c38d448cb7446b7b26cd0dc882976ba94dd3
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# [!DNL Adobe Target Profiles API] overzicht

[!DNL Adobe Target] maakt en onderhoudt een profiel voor elke individuele gebruiker. Dit profiel is opgeslagen op het tabblad [!DNL Target] edge-cluster en wordt na elk bezoek in real-time bijgewerkt.

## Structuur van een [!DNL Target] profiel

Een doelprofiel bestaat uit de volgende objecten:

| Object | Details |
| --- | --- |
| `clientcode` | De [!DNL Target] clientcode waaraan het profiel is gekoppeld. |
| `visitorId` | De id voor het profiel. Dit kan een `tntid`, `thirdpartyid`, of `marketingcloudvisitorid`. |
| `modifiedAt` | De tijdstempel van wanneer het profiel voor het laatst is bijgewerkt. |
| `profileAttributes` | Lijst met alle profielkenmerken die zijn opgeslagen als sleutel-waardeparen voor dat afzonderlijke profiel. |

### Voorbeeldprofielstructuur

```
{
    "client": "<your-tenant-name>",
    "visitorId": "a1-mbox3rdPartyId",
    "modifiedAt": "2017-08-18T17:53:39.003-04:00",
    "profileAttributes": {
        "insurance": {
            "value": "false",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "country": {
            "value": "france",
            "modifiedAt": "2017-07-31T14:26:30.879-04:00"
        },
        "checking": {
            "value": "true",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "user.memberlevel": {
            "value": "0.0",
            "modifiedAt": "2017-08-09T18:18:04.661-04:00"
        },
        "param1": {
            "value": "value1",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "param2": {
            "value": "value2",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "firstSessionStart": {
            "value": "1500648715286",
            "modifiedAt": "2017-07-21T10:51:55.286-04:00"
        },
        "entity.name": {
            "value": "my-entityName",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "entity.id": {
            "value": "my-entityId",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        }
    }
}
```
