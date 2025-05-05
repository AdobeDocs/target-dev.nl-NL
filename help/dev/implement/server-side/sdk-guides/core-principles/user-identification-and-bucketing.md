---
title: Gebruikersidentificatie en -registratie
description: Gebruikersidentificatie en -registratie
exl-id: 4fcf235b-6a58-442c-ae13-9d05ec1033fc
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 0%

---

# Gebruikersidentificatie en -registratie

## Gebruikersidentificatie

Er zijn meerdere manieren waarop een gebruiker kan worden geïdentificeerd binnen [!DNL Adobe Target]. [!UICONTROL Target] gebruikt de volgende id&#39;s:

| Veldnaam | Beschrijving |
| --- | --- |
| `tntID` | De `tntId` is de primaire id in [!DNL Target] voor een gebruiker. U kunt deze id opgeven, of [!DNL Target] automatisch genereren als de aanvraag geen verzoek bevat. |
| `thirdPartyId` | De `thirdPartyId` is het herkenningsteken van uw bedrijf voor de gebruiker, die u met elke vraag kunt verzenden. Wanneer een gebruiker zich bij de plaats van een bedrijf aanmeldt, leidt het bedrijf typisch tot een identiteitskaart die aan de rekening van de bezoeker, de loyaliteitskaart, het lidmaatschapsaantal, of andere toepasselijke herkenningstekens voor dat bedrijf gebonden is. |
| `marketingCloudVisitorId` | De `marketingCloudVisitorId` wordt gebruikt om gegevens tussen verschillende Adobe oplossingen samen te voegen en te delen. De marketingCloudVisitorId is vereist voor integratie met Adobe Analytics en Adobe Audience Manager. |
| `customerIds` | Samen met de Experience Cloud-bezoeker-id [klant-id&#39;s](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=nl-NL) en een voor authentiek verklaarde status voor elke bezoeker kan ook worden gebruikt. |

## [!DNL Target] ID (tntID)

De [!DNL Target] ID, of `tntId`, kan worden beschouwd als een apparaat-id. Dit `tntId` wordt automatisch gegenereerd door [!DNL Adobe Target] indien dit niet in het verzoek wordt vermeld. Verzoeken in een volgende fase moeten dit bevatten `tntId` om de juiste inhoud te kunnen leveren aan een apparaat dat door dezelfde gebruiker wordt gebruikt.

De volgende steekproefvraag toont een situatie aan waarin een `tntId` wordt niet doorgegeven aan [!DNL Target].

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
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

>[!TAB Java SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

Bij ontbreken van een `tntId`, [!DNL Adobe Target] genereert een `tntId` en geeft dit als volgt aan in het antwoord.

```json {line-numbers="true"}
{
  "status": 200,
  "requestId": "5b586f83-890c-46ae-93a2-610b1caa43ef",
  "client": "acmeclient",
  "id": {
      "tntId": "10abf6304b2714215b1fd39a870f01afc.35_0"
  },
  "edgeHost": "mboxedge35.tt.omtrdc.net",
  ...
}
```

In dit voorbeeld worden de gegenereerde `tntId` is `10abf6304b2714215b1fd39a870f01afc.35_0`. Let op dit `tntId` moet voor dezelfde gebruiker in verschillende sessies worden gebruikt.

## Id van derde partij (thirdPartyId)

Als uw organisatie een id gebruikt om uw bezoeker te identificeren, kunt u `thirdPartyID` om inhoud te leveren. A `thirdPartyID` is een permanente id die uw bedrijf gebruikt om een eindgebruiker te identificeren, ongeacht of deze via internet, mobiele of IoT-kanalen met uw bedrijf werkt. Met andere woorden: `thirdPartyId` verwijst naar gebruikersprofielgegevens die via kanalen kunnen worden gebruikt. U moet echter de `thirdPartyID` voor elke [!DNL Adobe Target] Aanroep van API voor levering die u maakt.

De volgende steekproefvraag toont het gebruik van aan `thirdPartyId`.

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      thirdPartyId: "B234A029348"
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

>[!TAB Java SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .thirdPartyId("B234A029348");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

In dit scenario: [!DNL Adobe Target] zal een `tntId` aangezien het niet in de originele vraag werd overgegaan, die aan verstrekt zal worden in kaart gebracht `thirdPartyId`.

## Bezoeker-id voor Marketing Cloud (MarketingCloudVisitorId)

De `marketingCloudVisitorId` is een universele en permanente id die uw bezoekers identificeert voor alle oplossingen in de Adobe Experience Cloud. Wanneer uw organisatie de id-service implementeert, kunt u met deze id dezelfde sitebezoeker en de bijbehorende gegevens identificeren in verschillende Experience Cloud-oplossingen, waaronder [!DNL Adobe Target], Adobe Analytics en Adobe Audience Manager. Let op: `marketingCloudVisitorId` is vereist bij integratie [!DNL Target] with [!DNL Adobe Analytics] en [!DNL Adobe Audience Manager].

De volgende steekproefvraag toont aan hoe een `marketingCloudVisitorId` die van de Dienst van identiteitskaart van Experience Cloud werd teruggewonnen wordt overgegaan tot [!DNL Target].

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      marketingCloudVisitorId: "10527837386392355901041112038610706884"
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

>[!TAB Java SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

In dit scenario: [!DNL Target] zal een `tntId` aangezien het niet in de originele vraag werd overgegaan, die aan verstrekt zal worden in kaart gebracht `marketingCloudVisitorId`.

## Klant-id (customerIds)

[Klant-id&#39;s](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=nl-NL) kan worden toegevoegd aan of gekoppeld aan een Experience Cloud-bezoeker-id. Wanneer u `customerIds`de `marketingCloudVisitorId` moeten ook worden verstrekt. Bovendien kan een authentificatiestatus samen met elk worden verstrekt `customerId` voor elke bezoeker. De volgende verificatiestatus kan worden gebruikt:

| Status van verificatie | Gebruikersstatus |
| --- | --- |
| `unknown` | Onbekend of nooit geverifieerd. Deze status kan worden gebruikt voor scenario&#39;s zoals die waarin een bezoeker op uw site landt door op een weergaveadvertentie te klikken. |
| `authenticated` | De gebruiker is momenteel geverifieerd met een actieve sessie op uw website of app. |
| `logged_out` | De gebruiker werd voor authentiek verklaard maar actief het programma geopend. De gebruiker was van plan om van de voor authentiek verklaarde staat los te maken. De gebruiker wil niet meer worden beschouwd als geverifieerd. |

Houd er rekening mee dat alleen `customerId` is in een voor authentiek verklaarde staat zal [!DNL Target] verwijzen naar de gegevens van het gebruikersprofiel die zijn opgeslagen en gekoppeld aan de customerId. Als de `customerId` zich in een onbekend of `logged_out` status, wordt deze genegeerd en worden eventuele gebruikersprofielgegevens gekoppeld aan die status `customerId` wordt niet gebruikt voor doelgerichte doelgroepen.

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      marketingCloudVisitorId : "10527837386392355901041112038610706884",
      customerIds: [{
        id: "134325423",
        integrationCode : "crm_data",
        authenticatedState : "authenticated"
      }]
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

>[!TAB Java SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

CustomerId customerId = new CustomerId()
  .id("134325423")
  .integrationCode("crm_data")
  .authenticatedState(AuthenticatedState.AUTHENTICATED);
VisitorId id = new VisitorId()
  .marketingCloudVisitorId("10527837386392355901041112038610706884")
  .customerIds(Arrays.asList(customerId));
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

In het bovenstaande voorbeeld ziet u hoe u een `customerId` met een `authenticatedState`. Wanneer u een `customerId`de `integrationCode`, `id`, en `authenticatedState` en de `marketingCloudVisitorId` zijn vereist. De `integrationCode` is de alias van de [klantkenmerkbestand](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=nl-NL) via CRS.

## Samengevoegd profiel

U kunt `tntId`, `thirdPartyID`, en `marketingCloudVisitorId` in hetzelfde verzoek. In dit scenario: [!DNL Adobe Target] Hiermee wordt de toewijzing van al deze id&#39;s behouden en vastgezet aan een bezoeker. Meer informatie over profielen [samengevoegd en in real time gesynchroniseerd](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=nl-NL) de verschillende id&#39;s gebruiken.

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId: "B234A029348",
      marketingCloudVisitorId : "10527837386392355901041112038610706884"
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

>[!TAB Java SDK]

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

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

In het bovenstaande voorbeeld ziet u hoe u kunt combineren `tntId`, `thirdPartyID`, en `marketingCloudVisitorId` in hetzelfde verzoek.

## Emmertje

Uw gebruikers worden ingesloten in het zien van een ervaring afhankelijk van hoe u opstelling uw [!DNL Adobe Target] activiteiten. In [!DNL Adobe Target], &quot;bucketing&quot;:

* **deterministisch**: MurmurHash3 wordt gebruikt om ervoor te zorgen dat uw gebruiker wordt gepompt en de juiste variatie elke keer ziet zolang de gebruiker - identiteitskaart verenigbaar is.
* **Vast**: [!DNL Adobe Target] slaat de variatie op die uw gebruiker in het gebruikersprofiel ziet om ervoor te zorgen dat de variatie aan die gebruiker over zittingen en kanalen constant wordt getoond. Variaties en kleverheid worden gegarandeerd bij het gebruik van beslissingen op de server. Bij gebruik van een apparaatbeslissing is kleverigheid niet gegarandeerd.

## Workflow van begin tot eind

Alvorens in het daadwerkelijke boekingsalgoritme te duiken, is het belangrijk om te benadrukken dat de gelijkaardige stappen zowel worden gebruikt om activiteiten te selecteren die op hun percentage van verkeerstoewijzing worden gebaseerd, als een ervaring binnen een activiteit te selecteren.

### Activiteit selecteren

1. Een apparaat-id genereren, meestal een UUID
1. De clientcode ophalen
1. De activiteiten-id ophalen
1. De salt ophalen, wat doorgaans een tekenreeks is als &quot;activity&quot;
1. De hash berekenen met gebruik van MurmurHash3
1. Hiermee wordt de absolute waarde van de hash opgehaald
1. De absolute waarde van de hash delen door 10000
1. Verdeel de rest door 10000, die een waarde tussen 0 en 1 zou moeten produceren
1. Vermenigvuldig het resultaat met 100%
1. Vergelijk het toewijzingspercentage van het activiteitenverkeer met het verkregen percentage. Als het percentage van de verkeerstoewijzing lager is, dan wordt de activiteit geselecteerd. Anders wordt de activiteit overgeslagen.

### Selectiestappen ervaren

1. Een apparaat-id genereren, meestal een UUID
1. De clientcode ophalen
1. De activiteiten-id ophalen
1. De salt ophalen, wat meestal een tekenreeks is als &quot;experience&quot;
1. De hash berekenen met gebruik van MurmurHash3
1. Hiermee wordt de absolute waarde van de hash opgehaald
1. De absolute waarde van de hash delen door 10000
1. Verdeel de rest door 10000, die een waarde tussen 0 en 1 zou moeten produceren
1. Vermenigvuldig het resultaat met het totale aantal ervaringen binnen de activiteit
1. Rond het resultaat af. Dit zou de ervaringsindex moeten produceren.

### Voorbeeld

Stel dat:

* Client C met clientcode `acmeclient`
* Activiteit A die identiteitskaart heeft `1111` en drie ervaringen `E1`, `E2`, `E3`
* De ervaring heeft de volgende distributie: `E1` - 33%, `E2` - 33%, `E3` - 34%

De selectiestroom ziet er als volgt uit:

1. Apparaat-id `702ff4d0-83b1-4e2e-a0a6-22cbe460eb15`
1. Clientcode `acmeclient`
1. Activiteits-id `1111`
1. Zout `experience`
1. Waarde voor hash `acmeclient.1111.702ff4d0-83b1-4e2e-a0a6-22cbe460eb15.experience`, hash-waarde `-919077116`
1. Absolute waarde van de hash `919077116`
1. Herinnering na de splitsing door 10000, `7116`
1. Waarde na de rest wordt gedeeld door 10000, `0.7116`
1. Resultaat na vermenigvuldiging van de waarde met het totale aantal ervaringen `3 * 0.7116 = 2.1348`
1. De ervaringsindex is `2`, dat wil zeggen de derde ervaring, aangezien wij `0` gebaseerd indexeren.
