---
keywords: adobe.target.getOffers, getOffers, getoffers, get aanbiedingen, at.js, functions, function, $8
description: Gebruik de [!UICONTROL adobe.target.getOffers()] functie en zijn opties voor de { [!DNL Adobe Target]  at.js bibliotheek om verzoeken in brand te steken om veelvoudige  [!DNL Target]  aanbiedingen te krijgen. (om 2.x.js)
title: Hoe gebruik ik de functie [!UICONTROL adobe.target.getOffers()] ?
feature: at.js
exl-id: b96a3018-93eb-49e7-9aed-b27bd9ae073a
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 0%

---

# [!UICONTROL adobe.target.getOffers()] - at.js 2.x

Deze functie laat u veelvoudige aanbiedingen terugwinnen door in veelvoudige dozen over te gaan. Bovendien kunnen meerdere aanbiedingen worden opgehaald voor alle weergaven in actieve activiteiten.

>[!NOTE]
>
>Deze functie is geïntroduceerd met at.js 2.x. Deze functie is niet beschikbaar voor versie 1 van at.js.*x*.

| Sleutel | Type | Vereist? | Beschrijving |
| --- | --- | --- | --- |
| `consumerId` | String | Nee | De standaardwaarde is het globale mbox van de cliënt als niet verstrekt. Deze sleutel wordt gebruikt om de supplementaire gegevens ID (SDID) te produceren die voor integratie A4T wordt gebruikt.<P>Bij gebruik van `getOffers()` genereert elke aanroep een nieuwe SDID. Als er meerdere box-aanvragen op dezelfde pagina staan en u wilt de SDID behouden (zodat deze overeenkomt met de SDID van de target-global-mbox en de [!DNL Adobe Analytics] SDID), gebruikt u de parameter `consumerId` .<P>Als `getOffers()` drie vakken bevat (genaamd &quot;mbox1&quot;, &quot;mbox2&quot; en &quot;mbox3&quot;), neemt u het volgende op: `consumerId: "mbox1, mbox2, mbox3"` in de `getOffers()` -aanroep. |
| `decisioningMethod` | String | Nee | &quot;server-side&quot;, &quot;on-device&quot;, &quot;hybride&quot; |
| `request` | Object | Ja | Zie onderstaande tabel Verzoeken. |
| `timeout` | Getal | Nee | Verzoek time-out. Als deze niet is opgegeven, wordt de standaardtime-out at.js gebruikt. |

## Verzoek

>[!NOTE]
>
>Raadpleeg de [ documentatie van API van de Levering ](/help/dev/implement/delivery-api/overview.md) voor informatie over de aanvaardbare types voor alle hieronder vermelde gebieden.

| Veldnaam | Vereist? | Beperkingen | Beschrijving |
| --- | --- | --- | --- |
| request > id | Nee |  | Een van `tntId`, `thirdPartyId` of `marketingCloudVisitorId` is vereist. |
| Request > id > thirdPartyId | Nee | Maximale grootte = 128. |  |
| Verzoek > ExperienceCloud | Nee |  |  |
| Request > ExperienceCloud > Analytics | Nee |  | Adobe Analytics-integratie |
| Request > ExperienceCloud > Analytics > logging | Nee | Het volgende moet op pagina worden geïmplementeerd:<ul><li>Bezoekersidentiteitsservice</li><li>Appmeasurement.js</li></ul> | De volgende waarden worden ondersteund:<P>**client_side**: Wanneer gespecificeerd, zal een analytische lading aan de bezoeker zijn teruggekeerd die zou moeten worden gebruikt om naar [!UICONTROL Adobe Analytics] via [!UICONTROL Data Insertion API] te verzenden.<P>**server_side**: Dit is de standaardwaarde waar [!DNL Target] en [!DNL Analytics] backend SDID zal gebruiken om de vraag voor rapporteringsdoeleinden samen te binden. |
| Verzoek > prefetch | Nee |  |  |
| Verzoek > Prefetch > views | Nee | Maximaal aantal 50.<P>Naam niet leeg.<P>Naam lengte `<=` 128.<P>Waarde length `<=` 5000.<P>De naam mag niet beginnen met &quot;profiel&quot;.<P>Namen niet toegestaan: &quot;orderId&quot;, &quot;orderTotal&quot;, &quot;productPurchasedId&quot;. | Geef parameters door die moeten worden gebruikt om relevante weergaven in actieve activiteiten op te halen. |
| Request > prefetch > views > profileParameters | Nee | Maximumaantal 50.<P>Naam niet leeg.<P>Naam lengte `<=` 128.<P>Waarde length `<=` 5000.<P>Accepteert alleen tekenreekswaarden.<P>De naam mag niet beginnen met &quot;profiel&quot;. | Geef profielparameters door die moeten worden gebruikt om relevante weergaven in actieve activiteiten op te halen. |
| Request > prefetch > views > product | Nee |  |  |
| Verzoek > Prefetch > views > product -> id | Nee | Niet leeg.<P>maximale grootte = 128. | Geef de product-id&#39;s door die moeten worden gebruikt om relevante weergaven in actieve activiteiten op te halen. |
| Request > prefetch > views > product > categoryId | Nee | Niet leeg.<P>maximale grootte = 128. | Geef de id&#39;s van de productcategorie door die moeten worden gebruikt om relevante weergaven in de activiteiten op te halen. |
| Request > prefetch > views > order | Nee |  |  |
| Request > prefetch > views > order > id | Nee | Maximumlengte = 250. | Geef dit door zodat id&#39;s kunnen worden gebruikt om relevante weergaven in actieve activiteiten op te halen. |
| Verzoek > Prefetch > views > order > total | Nee | Totaal `>=` 0. | Geef de totalen door die moeten worden gebruikt om relevante weergaven in actieve activiteiten op te halen. |
| Request > prefetch > views > order > purchaseProductIds | Nee | Geen lege waarden.<P>Maximale lengte van elke waarde 50.<P>Samengevoegd en gescheiden door komma.<P>Totale lengte van product-id&#39;s `<=` 250. | Geef de aangeschafte product-id&#39;s door die moeten worden gebruikt om relevante weergaven in actieve activiteiten op te halen. |
| Verzoek > Uitvoeren | Nee |  |  |
| Verzoek > Uitvoeren > pageLoad | Nee |  |  |
| Request > execute > pageLoad > parameters | Nee | Maximaal aantal 50.<P>Naam niet leeg.<P>Naam lengte `<=` 128.<P>Waarde length `<=` 5000.<P>Accepteert alleen tekenreekswaarden.<P>De naam mag niet beginnen met &quot;profiel&quot;.<P>Namen niet toegestaan: &quot;orderId&quot;, &quot;orderTotal&quot;, &quot;productPurchasedId&quot;. | Haal aanbiedingen met de opgegeven parameters op wanneer de pagina wordt geladen. |
| Verzoek > execute > pageLoad > profileParameters | Nee | Maximaal aantal 50.<P>Naam niet leeg.<P>Naam lengte `<=` 128.<P>De lengte van de waarde `<=` {256.<P>De naam mag niet beginnen met &quot;profiel&quot;.<P>Accepteert alleen tekenreekswaarden. | Haal aanbiedingen met de opgegeven profielparameters op wanneer de pagina wordt geladen. |
| Request > execute > pageLoad > product | Nee |  |  |
| Verzoek > execute > pageLoad > product -> id | Nee | Niet leeg.<P>Maximale grootte = 128. | Ontvang voorstellen met gespecificeerde product IDs wanneer de pagina laadt. |
| Request > execute > pageLoad > product > categoryId | Nee | Niet leeg.<P>Maximale grootte = 128. | Ontvang voorstellen met gespecificeerde productcategorie IDs wanneer de pagina laadt. |
| Verzoek > execute > pageLoad > order | Nee |  |  |
| Verzoek > execute > pageLoad > order > id | Nee | Maximumlengte = 250. | Ontvang voorstellen met gespecificeerde orde IDs wanneer de pagina laadt. |
| Verzoek > execute > pageLoad > order > total | Nee | `>=` 0 | Ontvang voorstellen met gespecificeerde ordetotalen wanneer de pagina laadt. |
| Verzoek > execute > pageLoad > order > purchaseProductIds | Nee | Geen lege waarden.<P>Maximale lengte van elke waarde 50.<P>Samengevoegd en gescheiden door komma.<P>Totale lengte van product-id&#39;s `<=` 250. | Ontvang voorstellen met gespecificeerde gekochte product IDs wanneer de pagina laadt. |
| Verzoek > Uitvoeren > Selecties | Nee | Maximale grootte = 50.<P>Geen null-elementen. |  |
| Request > execute > mboxes>mbox | Ja | Niet leeg.<P>Geen achtervoegsel &#39;-geklikt&#39;.<P>Maximale grootte = 250.<P>Toegestane tekens: `'-, ._\/=:;&!@#$%^&*()_+|?~[]{}'`\|Naam van vak. |
| Request > execute > boxes>mbox>index | Ja | Niet null.<P>Uniek.<P>`>=` 0 | De index vertegenwoordigt niet de volgorde waarin de vakken worden verwerkt. Net als in een webpagina met verschillende regionale vakken kan de volgorde waarin ze worden verwerkt niet worden opgegeven. |
| Request > execute > boxes > mbox > parameters | Nee | Maximum aantal = 50.<P>Naam niet leeg.<P>Naam lengte `<=` 128.<P>Accepteert alleen tekenreekswaarden.<P>Waarde length `<=` 5000.<P>De naam mag niet beginnen met &#39;profiel&#39;.<P>Namen niet toegestaan: &quot;orderId&quot;, &quot;orderTotal&quot;, &quot;productPurchasedId&quot;. | Hiermee worden voorstellen voor een bepaalde mbox met de opgegeven parameters opgehaald. |
| Verzoek > execute > mboxes>mbox>profileParameters | Nee | Maximum aantal = 50.<P>Naam niet leeg.<P>Naam lengte `<=` 128.<P>Accepteert alleen tekenreekswaarden.<P>De lengte van de waarde `<=` {256.<P>De naam mag niet beginnen met &#39;profiel&#39;. | Hiermee worden aanbiedingen voor een bepaalde box met de opgegeven profielparameters opgehaald. |
| Request > execute > mboxes>mbox > product | Nee |  |  |
| Request > execute > boxes > mbox > product > id | Nee | Niet leeg.<P>Maximale grootte = 128. | Wis voorstellen voor een bepaalde doos met gespecificeerde product IDs. |
| Verzoek > Uitvoeren > Selectievakje > Product > Categorie-id | Nee | Niet leeg.<P>Maximale grootte = 128. | Wis voorstellen voor een bepaalde doos met gespecificeerde productcategorie IDs. |
| Request > execute > boxes > mbox > order | Nee |  |  |
| Request > execute > boxes>mbox > order > id | Nee | Maximumlengte = 250. | Haal voorstellen voor een bepaalde mbox met de gespecificeerde orde IDs op. |
| Verzoek > Uitvoeren > Vakken > Postvak > Volgorde > Totaal | Nee | `>=` 0 | Wis voorstellen voor een bepaalde mbox met de gespecificeerde orde totalen. |
| Verzoek > execute > boxes > mbox > order > purchaseProductIds | Nee | Geen lege waarden.<P>De maximumlengte van elke waarde = 50.<P>Samengevoegd en gescheiden door komma.<P>Product ids totale lengte `<=` 250. | Wis voorstellen voor een bepaalde doos met de gespecificeerde orde gekochte product IDs. |

## Roep [!UICONTROL getOffers()] aan voor alle weergaven

```javascript {line-numbers="true"}
adobe.target.getOffers({
    request: {
      prefetch: {
        views: [{}]
    }
  }
});
```

## Roep [!UICONTROL getOffers()] aan om een beslissing op het apparaat te maken

```javascript {line-numbers="true"}
adobe.target.getOffers({ 

  decisioningMethod:"on-device", 
  request: { 
    execute: { 
      mboxes: [ 
        { 
          index: 0, 
          name: "homepage" 
        } 
      ] 
    } 
 } 
}); 
```

## Roep [!UICONTROL getOffers()] aan om de recentste meningen met de overgegaan parameters en profielparameters terug te winnen

```javascript {line-numbers="true"}
adobe.target.getOffers({
  request: {
    "prefetch": {
      "views": [
        {
          "parameters": {
            "ad": "1"
          },
          "profileParameters": {
            "age": 23
          }
        }
      ]
    }
  }
});
```

## Roep [!UICONTROL getOffers()] aan om dozen met doorgegeven parameters en profielparameters terug te winnen.

```javascript {line-numbers="true"}
adobe.target.getOffers({
  request: {
    execute: {
      mboxes: [
        {
          index: 0,
          name: "first-mbox"
        },
        {
          index: 1,
          name: "second-mbox",
          parameters: {
            a: 1
          },
          profileParameters: {
            b: 2
          }
        }
      ]
    }
  }
});
```

## Roep [!UICONTROL getOffers()] aan om de lading van de analytische lading van de cliëntkant terug te winnen

```javascript {line-numbers="true"}
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

**Reactie**:

```javascript {line-numbers="true"}
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

De nuttige lading kan dan aan [!DNL Adobe Analytics] via de [ Invoeging API van Gegevens ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) door:sturen.

## Gegevens uit meerdere vakken ophalen en renderen via [!UICONTROL getOffers()] en [!UICONTROL applyOffers()]

Met at.js 2.x kunt u meerdere vakken ophalen via de `[!UICONTROL getOffers()]` API. U kunt ook gegevens ophalen voor meerdere vakken en vervolgens met `[!UICONTROL applyOffers()]` de gegevens renderen op verschillende locaties die door een CSS-kiezer worden geïdentificeerd.

In het volgende voorbeeld ziet u een eenvoudige HTML-pagina waarop at.js 2.x is geïmplementeerd:

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>at.js 2.x, multiple selectors and multiple mboxes</title>
  <script src="at.js"></script>
</head>
<body>
  <div id="container1">Default content 1</div>
  
  <div id="container2">Default content 2</div>

  <div id="container3">Default content 3</div>
</body>
</html>
```

Stel dat u drie containers hebt die u wilt wijzigen via inhoud die u van [!DNL Target] hebt ontvangen. U kunt één aanvraag maken voor drie vakken waarin elke box inhoud bevat die in de desbetreffende container moet worden gerenderd.

De aanvraag- en rendercode kunnen er als volgt uitzien:

```javascript {line-numbers="true"}
adobe.target.getOffers({
  request: {
    prefetch: {
      mboxes: [
        {
          index: 0,
          name: "mbox1"
        },
        {
          index: 1,
          name: "mbox2"
        },
        {
          index: 2,
          name: "mbox3"
        }
      ]
    }
  }
})
.then(response => {
  // get all mboxes from response
  const mboxes = response.prefetch.mboxes;
  let count = 1;

  mboxes.forEach(el => {
    adobe.target.applyOffers({
      selector: "#container" + count,
      response: {
        prefetch: {
          mboxes: [el]
        }
      }
    });

    count += 1;
  });
});
```

In de sectie `request > prefetch > mboxes` zijn er drie verschillende vakken. Als de aanvraag is voltooid, ontvangt u de reactie voor elke box van `response > prefetch > mboxes` . Nadat u de reacties hebt en de locaties die u voor rendering wilt gebruiken, kunt u `applyOffers()` aanroepen om de inhoud te renderen die u hebt opgehaald uit [!DNL Target] . In dit voorbeeld hebben we de volgende afbeelding:

* mbox1 > CSS selector #container1
* mbox2 > CSS selector #container2
* mbox3 > CSS selector #container3

In dit voorbeeld wordt de telvariabele gebruikt om de CSS-kiezers samen te stellen. In een real-life scenario kunt u een verschillende afbeelding gebruiken tussen de CSS-kiezer en de box.

In dit voorbeeld wordt `prefetch > mboxes` gebruikt, maar u kunt `execute > mboxes` ook gebruiken. Als u de voorinstelling in `getOffers()` gebruikt, moet u ook de voorinstelling in de `applyOffers()` -aanroep gebruiken.

## Roep [!UICONTROL getOffers()] aan om een pageLoad uit te voeren

In het volgende voorbeeld ziet u hoe u een pageLoad uitvoert met [!UICONTROL getOffers()] met at.js 2.*x*

```javascript {line-numbers="true"}
adobe.target.getOffers({
    request: {
        execute: {
            pageLoad: {
                parameters: {}
            }
        }
    }
});
```
