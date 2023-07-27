---
keywords: mobiele app , mobiele app sdk , mobiele app , mobiele doeltoepassing , mobiele doelSDK , mobiele app sdk , inschakelen doel in sdk
description: Leer hoe u de Adobe Mobile Services SDK toevoegt aan uw mobiele app.
title: Procedures inschakelen [!DNL Target] in de [!DNL Adobe Mobile SDK]?
feature: Implement Mobile
exl-id: 4263b96a-23c8-4513-8302-00080122181d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Inschakelen [!DNL Target] in de SDK

Voeg de [!UICONTROL Adobe Mobile Services SDK] naar uw app.

>[!IMPORTANT]
>
>Steun voor de [!DNL Adobe Mobile] versie 4.*x* SDK&#39;s zijn geëindigd op 31 augustus 2021 en worden niet langer aanbevolen voor [!DNL Adobe Target] mobiele gebruikers.
>
>De [Adobe Experience Platform SDK voor mobiele apps](https://developer.adobe.com/client-sdks/documentation/){target=_blank} is de aanbevolen oplossing voor stroom [!DNL Adobe Experience Cloud] oplossingen en services in uw mobiele apps.

1. Als u de SDK van Adobe Mobile Services niet hebt geïnstalleerd in uw app, gebruikt u uw Analytics- of Experience Cloud-gegevens en downloadt u de SDK via de [Adobe mobiele services](https://mobilemarketing.adobe.com/) website.

1. Voeg de [!DNL Adobe Mobile Services SDK] naar uw app.

   U vindt de instructies onder [Core-implementatie en levenscyclus](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/dev-qs.html).

1. Voeg cliëntcode toe, onderbreking en laat SSL toe.

   Open Mobiele services in de Experience Cloud en ga vervolgens naar **[!UICONTROL Manage App Settings]** > **[!UICONTROL SDK Target Options]**.

   Voeg uw [!DNL Target] clientcode en time-out. De clientcode is uniek voor uw account of bedrijf. De time-out is de tijd in het aantal seconden tot [!DNL Target] wacht op een reactie voordat de standaardinhoud wordt weergegeven. Zorg ervoor dat de **[!UICONTROL Use HTTPS]** Deze optie is ingeschakeld op de pagina Toepassingsinstellingen beheren in Adobe Mobile Services. Als HTTPS niet wordt toegelaten, zullen alle vraag in iOS9+ worden geblokkeerd tenzij u voegt op lijst van gewenste personen [!DNL Target] server.

   ![alternatieve afbeelding](assets/mobile-clientcode.png)

1. Nadat u de app hebt gemaakt/gevonden, zoekt u de app-instellingen en downloadt u de gewenste SDK.

   ![alternatieve afbeelding](assets/download-sdk.png)

>[!WARNING]
>
> Als u geen toegang hebt tot de mobiele marketinginterface, kunt u rechtstreeks wijzigingen aanbrengen in het configuratiebestand in uw toepassingscode. De wijzigingen zijn echter niet synchroon met de instellingenpagina in de gebruikersinterface.
