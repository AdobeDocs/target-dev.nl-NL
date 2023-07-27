---
title: Hoe te om asynchrone verzoeken in te gebruiken [!DNL Adobe Target] .NET SDK
description: Meer informatie [!DNL Target] Java SDK ondersteunt asynchrone aanvragen, waardoor de effectieve doeltijd tot nul kan worden teruggebracht.
feature: APIs/SDKs
exl-id: fd36cc7b-a884-4e57-93c2-8aff8256109a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Asynchrone verzoeken (.NET)

## Beschrijving

Een voordeel van integratie aan de serverzijde is dat je de enorme bandbreedte en computerbronnen die beschikbaar zijn aan de serverzijde kunt benutten door parallellisme te gebruiken. [!DNL Target] .NET SDK steunt asynchrone verzoeken, die het gemakkelijk maken om te integreren [!DNL Target] in de bestaande asynchrone workflow van een app.

## Ondersteunde methoden

### \.NET

```dotnet {line-numbers="true"}
Task<TargetDeliveryResponse> GetOffersAsync(TargetDeliveryRequest request);
Task<TargetDeliveryResponse> SendNotificationsAsync(TargetDeliveryRequest request);
Task<TargetAttributes> GetAttributesAsync(TargetDeliveryRequest request, params string[] mboxes);
```

## Voorbeeld

Een voorbeeld van het gebruik van de asynchrone SDK-API kan er als volgt uitzien:

### \.NET

```dotnet {line-numbers="true"}
var deliveryRequest = new TargetDeliveryRequest.Builder()
    .SetExecute(new ExecuteRequest(mboxes: new List<MboxRequest> { new MboxRequest(index: 1, name: "a1-serverside-ab") }))
    .Build();

var response = await this.targetClient.GetOffersAsync(deliveryRequest);

var notificationRequest = new TargetDeliveryRequest.Builder()
    .SetSessionId(response.Request.SessionId)
    .SetTntId(response.Response?.Id?.TntId)
    .SetNotifications(new List<Notification>
        {
            new (id: "1", type: MetricType.Display, timestamp: DateTimeOffset.UtcNow.ToUnixTimeMilliseconds(),
                mbox: new NotificationMbox("product1", "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"),
                tokens: new List<string> { "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" })
        })
    .Build();

var notificationResponse = await this.targetClient.SendNotificationsAsync(notificationRequest);
```

In dit voorbeeld wordt ervan uitgegaan dat u [geïnitialiseerd de SDK](initialize-sdk.md).
