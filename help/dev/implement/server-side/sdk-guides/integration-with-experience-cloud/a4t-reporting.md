---
title: Integratie met Experience Cloud A4T Reporting
description: Integratie met Experience Cloud, A4T-rapportage, Analyses voor doelintegratie
keywords: levering api, server-kant, server-kant, integratie, a4t
exl-id: 0d09d7a1-528d-4e6a-bc6c-f7ccd61f5b75
feature: Implement Server-side
source-git-commit: cbae0f1758fb0dee4837e8c237f8617ecb46eb25
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# [!UICONTROL Analytics for Target] (A4T) rapportage

[!DNL Adobe Target] ondersteunt A4T-rapporten voor zowel on-device-besluitvorming als server-side [!DNL Target] -activiteiten. Er zijn twee configuratieopties voor het inschakelen van A4T-rapporten:

* [!DNL Adobe Target] stuurt de analytische lading automatisch door naar [!DNL Adobe Analytics] , of
* De gebruiker vraagt de analytische lading van [!DNL Adobe Target]. ([!DNL Adobe Target] keert [!DNL Adobe Analytics] nuttige lading terug naar de bezoeker.)

>[!NOTE]
>
>Apparaatbeslissingen ondersteunen alleen A4T-rapportage waarvan [!DNL Adobe Target] de lading van de analytische gegevens automatisch doorstuurt naar [!DNL Adobe Analytics] . Het ophalen van de analytische lading van [!DNL Adobe Target] wordt niet ondersteund.

## Voorwaarden

1. Configureer de activiteit in de [!DNL Adobe Target] gebruikersinterface met [!DNL Adobe Analytics] als bron voor rapportage en zorg ervoor dat de accounts zijn ingeschakeld voor A4T.
1. De API-gebruiker genereert de Adobe [!UICONTROL Marketing Cloud Visitor ID] en zorgt ervoor dat deze id beschikbaar is wanneer de [!DNL Target] -aanvraag wordt uitgevoerd.

## [!DNL Adobe Target] stuurt de [!DNL Analytics] payload automatisch door

[!DNL Adobe Target] kan de lading van de analytische lading automatisch doorsturen naar [!DNL Adobe Analytics] als de volgende herkenningstekens worden verstrekt:

1. `supplementalDataId`: De id die wordt gebruikt om te naaien tussen [!DNL Adobe Analytics] en [!DNL Adobe Target] . Als u wilt dat [!DNL Adobe Target] en [!DNL Adobe Analytics] gegevens op de juiste wijze aan elkaar koppelen, moet `supplementalDataId` dezelfde gegevens worden doorgegeven aan zowel [!DNL Adobe Target] als [!DNL Adobe Analytics] .
1. `trackingServer` : De [!DNL Adobe Analytics] -server.

>[!BEGINTABS]

>[!TAB  Node.js ]

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

>[!TAB  Java ]

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

Een gebruiker kan [!DNL Adobe Analytics] nuttige lading voor een bepaalde mbox terugwinnen, dan het verzenden naar [!DNL Adobe Analytics] via de [ Invoeging API van Gegevens ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md). Wanneer een [!DNL Adobe Target] -aanvraag wordt geactiveerd, geeft u `client_side` door aan het `logging` -veld in de aanvraag. Deze aanvraag retourneert een payload als het opgegeven mbox aanwezig is in een activiteit die [!DNL Analytics] als rapportagebron gebruikt.

>[!BEGINTABS]

>[!TAB  Node.js ]

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

>[!TAB  Java ]

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

Nadat u `logging = client_side` hebt opgegeven, ontvangt u de payload in het veld mbox.

Als de reactie van [!DNL Target] iets in de eigenschap `analytics -> payload` bevat, stuurt u deze door zoals deze naar [!DNL Adobe Analytics] is. [!DNL Adobe Analytics] weet hoe deze lading moet worden verwerkt. Dit kan in een GET-verzoek in de volgende notatie worden gedaan:

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/{content_type_num}/{code_ver}/{session}?pe=tnt&tnta={payload}&c.&a.&target.&sessionId={sessionId}&.target&.a&.c&mid={mid}
```

### Parameters en variabelen voor queryreeksen

| Veldnaam | Vereist | Beschrijving |
| --- | --- | --- |
| `rsid` | Ja | De rapportsuite-id |
| `content_type_num` | Ja | Altijd ingesteld op 0 |
| `code_ver` | Ja | Altijd ingesteld op &quot;MOBILE-1.0&quot; |
| `session` | Ja | Altijd ingesteld op 0 |
| `pe` | Ja | Pagina-gebeurtenis. Altijd ingesteld op `tnt` |
| `tnta` | Ja | [!DNL Analytics] payload die door [!DNL Target] server wordt geretourneerd in `analytics -> payload -> tnta` |
| `sessionId` | Ja | [!DNL Target] sessie-id van de actieve sessie |
| `mid` | Ja | Marketing Cloud-bezoeker-id |

### Vereiste koptekstwaarden

| Naam koptekst | Waarde koptekst |
| --- | --- |
| Host | Server voor gegevensverzameling van analysemogelijkheden (bijv. `adobeags421.sc.omtrdc.net`) |

### Voorbeeld van A4T gegevens invoegen HTTP ophalen oproep

Niet-URL-gecodeerde versie voor leesbaarheid (indeling wordt niet gebruikt voor API-aanroepen):

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0/0?tnta=253236:0:0|0,253236:0:0|2,253236:0:0|1,253613:0:0|0,253613:0:0|2,253613:0:0|1&c.&a.&target.&sessionId=45c08980-f4b9-4e11-96db-067d58e49f74&.target&.a&.c&pe=tnt&mid=69170113867710665996968872592584719577
```

URL-gecodeerde versie (indeling voor API-aanroepen):

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0/0?tnta=253236%3A0%3A0%7C0%2C253236%3A0%3A0%7C2%2C253236%3A0%3A0%7C1%2C253613%3A0%3A0%7C0%2C253613%3A0%3A0%7C2%2C253613%3A0%3A0%7C1&c.%26a.%26target.%26sessionId=45c08980-f4b9-4e11-96db-067d58e49f74%26.target%26.a%26.c&pe=tnt&mid=69170113867710665996968872592584719577 
```
