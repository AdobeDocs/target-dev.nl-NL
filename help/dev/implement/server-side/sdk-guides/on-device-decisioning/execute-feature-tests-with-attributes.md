---
title: Functietests uitvoeren met kenmerken
description: Functietests uitvoeren met kenmerken
feature: APIs/SDKs
exl-id: c89d337c-20a9-454c-930c-79d9217e23b6
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# Functietests uitvoeren met kenmerken

## Overzicht van de stappen

1. Inschakelen [!UICONTROL on-device decisioning] voor uw organisatie
1. Een [!UICONTROL A/B Test] activiteit
1. Geef uw A en B op
1. Een publiek toevoegen
1. Verkeerstoewijzing instellen
1. Verkeersdistributie instellen op variaties
1. Rapportage instellen
1. Metriek toevoegen voor het bijhouden van KPI&#39;s
1. Code implementeren om functietests met kenmerken uit te voeren
1. Code implementeren om conversiegebeurtenissen bij te houden
1. Tests met kenmerken voor uw functie activeren

>[!NOTE]
>
>Stel dat u een e-commercebedrijf voor de detailhandel bent. U wilt de conversiesnelheid verhogen wanneer klanten door de productcatalogus bladeren en deze doorzoeken. Er bestaat een hypothese dat bepaalde sorteeralgoritmen en pagineringsstrategieën betere resultaten opleveren dan andere. U kunt deze theorie testen door een functietest uit te voeren waarbij de sorteerwidget opnieuw wordt ontworpen met behulp van verschillende sorteeropties voor uw eindgebruikers. U wilt ervoor zorgen dat deze functietest wordt uitgevoerd met een latentie van bijna nul, zodat dit geen negatieve invloed heeft op de gebruikerservaring en de resultaten niet scheeftrekt.

## 1. Inschakelen [!UICONTROL on-device decisioning] voor uw organisatie

Het toelaten van op-apparatenbesluit verzekert een activiteit A/B bij bijna-nul latentie wordt uitgevoerd. Als u deze functie wilt inschakelen, navigeert u naar **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** in [!DNL Adobe Target]en de **[!UICONTROL On-Device Decisioning]** schakelen.

![alternatieve afbeelding](assets/asset-odd-toggle.png)

>[!NOTE]
>
>U moet de beheerder of fiatteur hebben [gebruikersrol](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) om de **[!UICONTROL On-Device Decisioning]** schakelen.

Nadat u het dialoogvenster **[!UICONTROL On-Device Decisioning]** schakelen, [!DNL Adobe Target] Beginnen met genereren *regelartefacten* voor uw client.

## 2. Maak een [!UICONTROL A/B Test] activiteit

1. In [!DNL Adobe Target], navigeert u naar de **[!UICONTROL Activities]** pagina, selecteert u vervolgens **[!UICONTROL Create Activity]** > **[!UICONTROL A/B test]**.

   ![alternatieve afbeelding](assets/asset-ab.png)

1. In de **[!UICONTROL Create A/B Test Activity]** modaal, verlaat het gebrek **[!UICONTROL Web]** geselecteerd (1), selecteert u **[!UICONTROL Form]** als uw ervaringscomposer (2), selecteert u **[!UICONTROL Default Workspace]** with **[!UICONTROL No Property Restrictions]** (3) en klikt u op **[!UICONTROL Next]** (4)

   ![alternatieve afbeelding](assets/asset-form.png)

## 3. Definieer uw A en B

1. In de **[!UICONTROL Experiences]** stap voor het maken van activiteiten, geef een naam op voor uw activiteit (1) en voeg een tweede ervaring toe, Experience B, door op de knop **[!UICONTROL Add Experience]** (2). Voer de naam in van de locatie (3) in de toepassing waar u de functietest met kenmerken wilt uitvoeren. In het onderstaande voorbeeld: `product-results-page` is de locatie die is gedefinieerd voor Experience A. (Dit is ook de locatie die is gedefinieerd voor Experience B.)

   ![alternatieve afbeelding](assets/asset-location.png)

   **[!UICONTROL Experience A]** zal JSON bevatten die uw bedrijfslogica signaleert om het volgende te doen:

   * De functie voor het sorteeralgoritme starten via het dialoogvenster `test_sorting` functiemarkering
   * Het aanbevolen sorteeralgoritme uitvoeren dat is gedefinieerd in het dialoogvenster `sorting_algorithm _**_attribute`
   * Retourneer 50 producten per pagina zoals gedefinieerd in de pagineringsstrategie die is gedefinieerd in het dialoogvenster `pagination_limit`

1. In Experience A klikt u om de inhoud te wijzigen vanuit **[!UICONTROL Default Content]** aan JSON door **[!UICONTROL Create JSON Offer]** zoals hieronder aangegeven (1).

   ![alternatieve afbeelding](assets/asset-offer.png)

1. De JSON definiëren met `test_sorting`, `sorting_algorithm`, en `pagination_limit` vlaggen en attributen die zullen worden gebruikt om het geadviseerde sorterende algoritme met een pagineringsgrens van 50 producten in werking te stellen.

   >[!NOTE]
   >
   >Wanneer [!DNL Adobe Target] emmert een gebruiker om Ervaring A te zien, JSON met de bepaalde attributen in het voorbeeld zal zijn teruggekeerd. In uw code, zult u de waarde van de eigenschapmarkering moeten controleren `test_sorting` om te zien of de sorteerfunctie moet worden ingeschakeld. Als dit het geval is, gebruikt u de aanbevolen waarde van de optie `sorting_algorithm` kenmerk om aanbevolen producten weer te geven in de lijstweergave van het product. De limiet van de producten die voor uw toepassing moeten worden weergegeven, is 50, aangezien dat de waarde van de `pagination_limit` kenmerk.

   ![alternatieve afbeelding](assets/asset-sorting.png)

   **[!UICONTROL Experience B]** zal JSON bepalen die uw bedrijfslogica signaleert om het volgende te doen:

   * De functie voor het sorteeralgoritme starten via de markering voor de functie test_sorting
   * Voer de `best_sellers` sorteeralgoritme gedefinieerd in het dialoogvenster `sorting_algorithm _**_attribute`
   * Retourneer 50 producten per pagina zoals gedefinieerd in de pagineringsstrategie die is gedefinieerd in het dialoogvenster `pagination_limit`

   >[!NOTE]
   >
   >Wanneer [!DNL Adobe Target] emmert een gebruiker om Ervaring B te zien, JSON met de bepaalde attributen in het voorbeeld zal zijn teruggekeerd. In uw code, zult u de waarde van de eigenschapmarkering moeten controleren `test_sorting` om te zien of de sorteerfunctie moet worden ingeschakeld. Als dat het geval is, gebruikt u de `best_sellers` waarde van de `sorting_algorithm` kenmerk voor de weergave van de productlijst met de beste verkochte producten. De limiet van de producten die voor uw toepassing moeten worden weergegeven, is 50, aangezien dat de waarde van de `pagination_limit` kenmerk.

   ![alternatieve afbeelding](assets/asset-sorting-b.png)

## 4. Voeg een publiek toe

In de **[!UICONTROL Targeting]** stap, de **[!UICONTROL All Visitors]** publiek. Hierdoor kunt u de invloed van uw sorteerfunctie begrijpen en ook begrijpen welke algoritme en het aantal items het beste invloed hebben op de resultaten.

![alternatieve afbeelding](assets/asset-audience-b.png)

## 5. Verkeerstoewijzing instellen

Definieer het percentage bezoekers op basis waarvan u de sorteeralgoritmen en pagineringsstrategie wilt testen. Met andere woorden, aan welk percentage van uw gebruikers wilt u deze test uitvoeren? In dit voorbeeld, om deze test aan alle het programma geopende gebruikers op te stellen, houd de verkeerstoewijzing bij 100%.

![alternatieve afbeelding](assets/asset-allocation-100.png)

## 6. Verkeersdistributie instellen op variaties

Bepaal het percentage bezoekers dat het aanbevolen versus het beste sorteeralgoritme voor verkopers ziet, met een limiet van 50 producten per pagina. In dit voorbeeld, houd de verkeersdistributie als 50/50 verdeling tussen Ervaringen A en B.

![alternatieve afbeelding](assets/asset-variations-50.png)

## 7. Rapportage instellen

In de **[!UICONTROL Goals & Settings]** stap, kies **[!UICONTROL Adobe Target]** als de **[!UICONTROL Reporting Source]** om uw A/B testresultaten in te zien [!DNL Adobe Target] UI of kies **[!UICONTROL Adobe Analytics]** om deze weer te geven in de gebruikersinterface van Adobe Analytics.

![alternatieve afbeelding](assets/asset-reporting-b.png)

## 8. Metriek toevoegen voor het bijhouden van KPI&#39;s

Kies een **[!UICONTROL Goal Metric]** om de eigenschapstest met attributen te meten. In dit voorbeeld, is het succes gebaseerd op of de gebruiker een product koopt, afhankelijk van het het sorteren algoritme en de pagineringsstrategie zij werden getoond.

## 9. Implementeer functietests met kenmerken in uw toepassing

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const options = {
  client: "testClient",
  organizationId: "ABCDEF012345677890ABCDEF0@AdobeOrg",
  decisioningMethod: "on-device",
  events: {
    clientReady: targetClientReady
  }
};
const targetClient = TargetClient.create(options);

function targetClientReady() {
  return targetClient.getAttributes(["product-results-page"]).then(function(attributes) {
    const test_sorting = attributes.getValue("product-results-page", "test-sorting");
    const sorting_algorithm = attributes.getValue("product-results-page", "sorting_algorithm");
    const pagination_limit = attributes.getValue("product-results-page", "pagination_limit");
  });
}
```

>[!TAB Java]

```java {line-numbers="true"}
import com.adobe.target.edge.client.ClientConfig;
import com.adobe.target.edge.client.TargetClient;
import com.adobe.target.delivery.v1.model.ChannelType;
import com.adobe.target.delivery.v1.model.Context;
import com.adobe.target.delivery.v1.model.ExecuteRequest;
import com.adobe.target.delivery.v1.model.MboxRequest;
import com.adobe.target.edge.client.entities.TargetDeliveryRequest;
import com.adobe.target.edge.client.model.TargetDeliveryResponse;

ClientConfig config = ClientConfig.builder()
    .client("testClient")
    .organizationId("ABCDEF012345677890ABCDEF0@AdobeOrg")
    .build();
TargetClient targetClient = TargetClient.create(config);
MboxRequest mbox = new MboxRequest().name("product-results-page").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
    .context(new Context().channel(ChannelType.WEB))
    .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
    .build();
Attributes attributes = targetClient.getAttributes(request, "product-results-page");
String testSorting = attributes.getString("product-results-page", "test-sorting");
String sortingAlgorithm = attributes.getString("product-results-page", "sorting_algorithm");
String paginationLimit = attributes.getString("product-results-page", "pagination_limit");
```

>[!ENDTABS]

## 10. Code implementeren om conversiegebeurtenissen te volgen

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity

//When a conversion happens
TargetClient.sendNotifications({
    targetCookie,
    "request" : {
      "notifications" : [
        {
          type: "click",
          timestamp : Date.now(),
          id: "conversion",
          mbox : {
            name : "product-results-page"
          }
        }
      ]
    }
})
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);

ExecuteRequest executeRequest = new ExecuteRequest();

NotificationDeliveryService notificationDeliveryService = new NotificationDeliveryService();

Notification notification = new Notification();
notification.setId("conversion");
notification.setImpressionId(UUID.randomUUID().toString());
notification.setType(MetricType.CLICK);
notification.setTimestamp(System.currentTimeMillis());
notification.setTokens(
    Collections.singletonList(
        "IbG2Jz2xmHaqX7Ml/YRxRGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="));

TargetDeliveryRequest targetDeliveryRequest =
    TargetDeliveryRequest.builder()
        .context(context)
        .execute(executeRequest)
        .notifications(Collections.singletonList(notification))
        .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
notificationDeliveryService.sendNotification(request);

Attributes attributes = targetClient.getAttributes(request, "product-results-page");
String testSorting = attributes.getString("product-results-page", "test-sorting");
String sortingAlgorithm = attributes.getString("product-results-page", "sorting_algorithm");
String paginationLimit = attributes.getString("product-results-page", "pagination_limit");
```

>[!ENDTABS]

## 11. Activeer de functietests met kenmerken

![alternatieve afbeelding](assets/asset-activate.png)
