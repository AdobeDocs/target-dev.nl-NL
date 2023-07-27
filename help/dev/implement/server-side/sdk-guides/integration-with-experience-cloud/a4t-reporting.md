---
title: Integratie met Experience Cloud A4T Reporting
description: Integratie met Experience Cloud, A4T-rapportage, Analyses voor doelintegratie
keywords: levering api, server-kant, server-kant, integratie, a4t
exl-id: 0d09d7a1-528d-4e6a-bc6c-f7ccd61f5b75
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# Analyses voor doelrapportage (A4T)

[!DNL Adobe Target] steunt A4T rapportering voor zowel op-apparatenbesluit als server-zijactiviteiten van het Doel. Er zijn twee configuratieopties voor het inschakelen van A4T-rapporten:

* [!DNL Adobe Target] stuurt de analytische lading automatisch door naar [!DNL Adobe Analytics], of
* De gebruiker vraagt de analytische lading van [!DNL Adobe Target]. ([!DNL Adobe Target] retourneert de [!DNL Adobe Analytics] nuttige lading terug naar de bezoeker.)

>[!NOTE]
>
>Besluiten op een apparaat ondersteunen alleen A4T-rapporten waarvan [!DNL Adobe Target] stuurt de analytische lading automatisch door naar [!DNL Adobe Analytics]. De analytische lading ophalen uit [!DNL Adobe Target] wordt niet ondersteund.

## Voorwaarden

1. Vorm de activiteit in [!DNL Adobe Target] UI met [!DNL Adobe Analytics] als de bron van de rapportage en ervoor zorgen dat de accounts zijn ingeschakeld voor A4T.
1. De API-gebruiker genereert de Adobe Marketing Cloud Visitor-id en zorgt ervoor dat deze id beschikbaar is wanneer de aanvraag voor het doel wordt uitgevoerd.

## [!DNL Adobe Target] De lading van Analytics automatisch doorsturen

[!DNL Adobe Target] kan de analytische lading automatisch doorsturen naar [!DNL Adobe Analytics] indien de volgende identificatiecodes worden verstrekt:

1. `supplementalDataId`: De id die wordt gebruikt om te schakelen tussen [!DNL Adobe Analytics] en [!DNL Adobe Target]. Om [!DNL Adobe Target] en [!DNL Adobe Analytics] om gegevens correct aan elkaar te binden, het zelfde `supplementalDataId` moet worden doorgegeven aan beide [!DNL Adobe Target] en [!DNL Adobe Analytics].
1. `trackingServer`: De [!DNL Adobe Analytics] Server.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {     
    id: {
      marketingCloudVisitorId : "2304820394812039",
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId:"23423432"
    },
    experienceCloud: {
      analytics: {
        logging: "server_side",
        supplementalDataId: "7D3AA246CC99FD7F-1B3DD2E75595498E",
        trackingServer: "jimsbrims.sc.omtrds.net"
      }
    }, 
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }       
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .tntId("d359234570e044f14e1faeeba02d6ab23439914e.35_0")
  .thirdPartyId("B234A029348")
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

AnalyticsRequest analyticsRequest =
    new AnalyticsRequest()
        .trackingServer("jimsbrims.sc.omtrds.net")
        .logging(LoggingType.SERVER_SIDE)
        .supplementalDataId("7D3AA246CC99FD7F-1B3DD2E75595498E");
ExperienceCloud expCloud =
    new ExperienceCloud()
        .setAnalytics(analyticsRequest);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .experienceCloud(expCloud)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

## Gebruiker haalt analytische lading op van [!DNL Adobe Target]

Een gebruiker kan de [!DNL Adobe Analytics] lading voor een bepaalde mbox, dan verzend het naar [!DNL Adobe Analytics] via de [API voor gegevensinvoer](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md). Wanneer een [!DNL Adobe Target] aanvraag is geactiveerd, doorgeven `client_side` aan de `logging` in de aanvraag. Dit zal een lading terugkeren als gespecificeerde mbox in een activiteit aanwezig is die Analytics als rapporteringsbron gebruikt.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};
const targetClient = TargetClient.create(CONFIG);
targetClient.getOffers({
  request: {     
    id: {
      marketingCloudVisitorId : "2304820394812039",
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId:"23423432"
    },
    experienceCloud: {
      analytics: {
        logging: "client_side"
      }
    },  
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }       
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .tntId("d359234570e044f14e1faeeba02d6ab23439914e.35_0")
  .thirdPartyId("B234A029348")
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

AnalyticsRequest analyticsRequest =
    new AnalyticsRequest()
        .logging(LoggingType.CLIENT_SIDE);
ExperienceCloud expCloud =
    new ExperienceCloud()
        .setAnalytics(analyticsRequest);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .experienceCloud(expCloud)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

Wanneer u `logging = client_side`, ontvangt u de lading in het mbox gebied.

Als de reactie van Doel iets in bevat `analytics -> payload` eigenschap, doorsturen naar de volgende [!DNL Adobe Analytics]. [!DNL Adobe Analytics] weet hoe deze lading moet worden verwerkt. Dit kan in een verzoek van de GET worden gedaan gebruikend het volgende formaat:

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/0/CODEVERSION?pe=tnt&tnta={payload}&mid={mid}&vid={vid}&aid={aid}
```

### Parameters en variabelen voor queryreeks

| Veldnaam | Vereist | Beschrijving |
| --- | --- | --- |
| `rsid` | Ja | De rapportsuite-id |
| `pe` | Ja | Pagina-gebeurtenis. Altijd instellen op `tnt` |
| `tnta` | Ja | Analyselading die door de server van het Doel in wordt geretourneerd `analytics -> payload -> tnta` |
| `mid` | Ja | Bezoeker-id Marketing Cloud |

### Vereiste koptekstwaarden

| Naam koptekst | Waarde koptekst |
| --- | --- |
| Host | Server voor gegevensverzameling voor analyse (bijv. `adobeags421.sc.omtrdc.net`) |

### Voorbeeld A4T Data Insertion HTTP Get Call

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0?pe=tnt&tnta=285408:0:0|2&mid=2304820394812039
```
