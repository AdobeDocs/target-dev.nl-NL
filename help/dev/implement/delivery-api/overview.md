---
title: Adobe Target Delivery API - Overzicht
description: Adobe Target Delivery API - Overzicht
keywords: aflevering api
exl-id: e760bddc-b1ae-4b7b-bff2-aba81c6b6d34
feature: APIs/SDKs
source-git-commit: ccc27e66207e58dcd33865e5d28a51644e8e1931
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Overzicht van de bezorgings-API

[!DNL Adobe Target Delivery API] is gebaseerd op REST. In deze documentatie worden de bronnen beschreven waaruit de [!DNL Adobe Target] [!DNL Delivery API] bestaat. De methodes van HTTP worden gebruikt om verrichtingen op die middelen uit te voeren.

Met [!UICONTROL Adobe Target's Delivery API] kunt u:

* Lever ervaringen over Web, met inbegrip van SPAs, en mobiele kanalen evenals niet browser gebaseerde IoT apparaten zoals aangesloten TV, kiosk, of in-store digitaal scherm.
* Lever ervaringen van om het even welke server zijplatform of toepassing die HTTP/s vraag kan maken.
* Lever verenigbare en gepersonaliseerde ervaringen aan een gebruiker ongeacht welke kanaal of apparaten de gebruiker met uw zaken in dienst heeft genomen.
* De ervaringen van het geheime voorgeheugen voor een gebruiker binnen een zitting in uw server zodat de veelvoudige API vraag kan worden vermeden en dientengevolge betere prestaties bereiken.
* Naadloos integreren met [!DNL Adobe Experience Cloud] -producten zoals [!DNL Adobe Analytics] , [!DNL Adobe Audience Manager] en [!DNL Experience Cloud ID Service] vanaf de serverzijde.

>[!IMPORTANT]
>
>Wees voorzichtig wanneer u [!DNL Recommendations] [!UICONTROL Catalog] via [!DNL Delivery API] bijwerkt. Het bestand [!DNL Delivery API] is public, gebruik dit dus niet om klikbare items in de catalogus met aanbevelingen te vullen. Zo kunt u ongeldig inhoud introduceren en uw catalogus vervuilen.
>
>Aanbevolen werkwijzen:
>
>Gebruik de [!DNL Delivery API] alleen voor het bijwerken van cataloguskenmerken die:
>* Verandering regelmatig (bijvoorbeeld prijs, voorraadniveau).
>* Volg een vooraf gedefinieerde indeling die gemakkelijk op uw website kan worden gevalideerd.
>* Gebruik deze optie niet voor het toevoegen of wijzigen van klikbare items of andere niet-geverifieerde inhoud.
>
>Indien nodig kunt u klantenondersteuning aanvragen om catalogusupdates uit te schakelen via de bezorgings-API.

Zie de [[!UICONTROL Adobe Target Delivery API] ](https://developer.adobe.com/target/implement/delivery-api/){target=_blank} documentatie voor meer informatie.

>[!NOTE]
>
>U kunt tot de [ erfenis /v1/mbox en /v2/batchmbox API documentatie ](https://developers.adobetarget.com/api/legacy-api/index.html) nog toegang hebben. Er worden echter functies ontwikkeld in de API voor levering (zoals hier beschreven) die niet worden teruggezet naar de bestaande API&#39;s.
