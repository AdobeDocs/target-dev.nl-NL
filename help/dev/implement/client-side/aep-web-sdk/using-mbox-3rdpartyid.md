---
title: Real-time profielsynchronisatie voor mbox3rdPartyId
description: Leer hoe te om mbox3rdPartyId met  [!DNL Adobe Experience Platform Web SDK] te gebruiken.
keywords: personalisatie;target;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
feature: AEP Web SDK
source-git-commit: 03b02fb87873d89c917c7a2d7e7f775b724ea083
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Wat is mbox3rdPartyId

De `mbox3rdPartyId` in [!DNL Adobe Target] is de bezoekersidentiteitskaart van uw bedrijf, zoals lidmaatschapsidentiteitskaart voor het loyaliteitsprogramma van uw bedrijf.

Wanneer een bezoeker zich aanmeldt bij de site van een bedrijf, maakt het bedrijf doorgaans een id die is gekoppeld aan de account, de loyaliteitskaart, het lidmaatschapsnummer of andere toepasselijke id&#39;s voor dat bedrijf. [ Leer meer ](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html)

## `mbox3rdPartyId` gebruiken met de [!DNL Platform Web SDK]

### Stap 1: Configureer de `Target Third Party ID Namespace`

Vorm `Target Third Party ID Namespace` in uw [ DataStream ](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview), gebruikend identiteitskaart Namespace u als 3de partijidentiteitskaart wilt gebruiken. [ Leer meer over identiteitskaart namespaces ](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html)

![ Experience Platform UI die het van de Derde van het Doel namespace gebied toont.](/help/dev/implement/client-side/aep-web-sdk/assets/mbox3rdpartyid.png)

### Stap 2: De `mbox3rdpartyId` naar [!DNL Target] verzenden

Verzend `mbox3rdpartyId` naar [!DNL Target] in het `sendEvent` bevel, gebruikend identiteitskaart namespace die u in Stap 1 vormde.
[ leer meer over het verzenden van IDs ](/help/dev/implement/client-side/aep-web-sdk/using-mbox-3rdpartyid.md)

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Replace `ID_NAMESPACE` with the namespace you have configured in Step 1.
        {
          "id": "1234",
          "authenticatedState": "authenticated"
        }
      ]
    }
  }
});
```
