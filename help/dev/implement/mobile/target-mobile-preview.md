---
keywords: qa, voorvertoning, voorvertoningskoppeling, mobiele voorvertoning
description: Gebruik koppelingen voor mobiele voorvertoningen om end-to-end kwaliteitscontroles uit te voeren voor mobiele toepassingsactiviteiten. U kunt zich inschrijven voor verschillende ervaringen zonder speciale testapparaten.
title: Hoe gebruik ik de koppeling Mobiele voorvertoning in [!DNL Target] Mobiel?
feature: Implement Mobile
exl-id: c0c4237a-de1f-4231-b085-f8f1e96afc13
source-git-commit: 97c96e63f9121793a83b445ad3dc33c5d094509a
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# [!DNL Target] mobiele voorvertoning

Gebruik de koppeling voor mobiele voorvertoningen om eenvoudige end-to-end QA&#39;s voor mobiele app-activiteiten uit te voeren en uzelf in te schrijven voor verschillende ervaringen op uw apparaat zonder speciale testapparaten.

## Overzicht

Met de functie voor mobiele voorvertoningen kunt u uw mobiele-toepassingsactiviteiten volledig testen voordat u deze live start.

## Vereisten

1. **Gebruik een ondersteunde versie van de SDK:** Voor de functie voor mobiele voorvertoningen moet u de juiste versie van de Adobe Mobile SDK downloaden en installeren in de corresponderende apps.

   Voor instructies voor het downloaden van de juiste SDK raadpleegt u [Huidige SDK-versies](https://developer.adobe.com/client-sdks/documentation/current-sdk-versions/){target=_blank} in de *[!DNL Adobe Experience Platform Mobile SDK]* documentatie.

1. **Een URL-schema instellen:** De voorbeeldkoppeling gebruikt een URL-schema om uw app te openen. U moet een uniek URL-schema opgeven voor de voorvertoning.

   Zie voor meer informatie [Visuele voorvertoning](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Adobe Target* in de *[!DNL Adobe Experience Platform Mobile SDK]* documentatie.

   De volgende koppelingen bevatten meer informatie:

   * **iOs**: Ga voor meer informatie over het instellen van URL-schema&#39;s voor iOS naar [Een aangepast URL-schema voor uw app definiëren](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target=_blank} op de Apple Developer-website.
   * **Android**: Ga voor meer informatie over het instellen van URL-schema&#39;s voor Android naar [Diepe koppelingen maken naar App-inhoud](https://developer.android.com/training/app-links/deep-linking){target=_blank} op de website van Android Developers.

1. **Instellen `collectLaunchInfo` API (alleen i0S)**

   Zie voor meer informatie [Visuele voorvertoning](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Adobe Target* in de *[!DNL Adobe Experience Platform Mobile SDK]* documentatie.

## Een voorbeeldkoppeling genereren

1. In de [!DNL Target] UI, klik **[!UICONTROL More Options]** pictogram (de verticale ellips) en selecteer vervolgens **[!UICONTROL Create Mobile Preview]**.

   ![alternatieve afbeelding](assets/mobile-preview-create.png)

1. Selecteer de activiteiten die u wilt voorvertonen en klik vervolgens op **[!UICONTROL Generate Mobile Preview Link]**.

   >[!NOTE]
   >
   >Alleen op formulieren gebaseerde AB- en XT-activiteiten kunnen worden geselecteerd.

   ![alternatieve afbeelding](assets/mobile-preview-select-activities.png)

1. Geef het URL-schema van uw app op.

   Dit moet hetzelfde zijn als wat er aanwezig is in uw iOS- of Android-app. Herhaal dit proces desgewenst afzonderlijk voor iOS en Android.

   ![alternatieve afbeelding](assets/mobile-preview-enter-url-scheme.png)

1. Klikken **[!UICONTROL Generate Mobile Preview Link]** en kopieert u de koppeling.

   ![alternatieve afbeelding](assets/mobile-preview-generate-and-copy.png)

## Voorvertonen op uw apparaat

Open de koppeling in een mobiele browser op een apparaat waarop uw app is geïnstalleerd. Deze app kan de productie-app zijn die u hebt gedownload van de Apple App Store of de Google Play Store. Het hoeft geen speciale build te zijn. Als u een actieve voorproefverbinding hebt, zult u de ervaringen op apparaat kunnen bekijken.

1. Open de koppeling in uw mobiele browser.

   Deel de koppeling die u in de vorige stap van de [!DNL Target] UI voor uw mobiele apparaat op een handige manier, bijvoorbeeld door tekst, e-mail of Slack te gebruiken.

   |![voorvertoning van diepe koppeling 1](assets/mobile-preview-open-deeplink.png)|![voorvertoning van diepe koppeling 2](assets/mobile-preview-open-app.png)|

   Uw app wordt geopend en start de [!DNL Target] Modus Mobiele voorvertoning.

1. Selecteer de combinatie van ervaringen die u wilt zien en klik op **[!UICONTROL Launch Experiences]**.

   |![mobiele voorvertoning 1](assets/mobile-preview-experience-selection-1.png)|![mobiele voorvertoning 2](assets/mobile-preview-experience-result-1-france.png)|![mobiele voorvertoning 3](assets/mobile-preview-experience-result-1-shipfree.png)| |![mobiele voorvertoning 4](assets/mobile-preview-experience-selection-2.png)|![mobiele voorvertoning 5](assets/mobile-preview-experience-result-2-aus.png)|![mobiele voorvertoning 6](assets/mobile-preview-experience-result-2-10off.png)|

## Beperkingen

* De nieuwe inhoud wordt pas na het dialoogvenster **[!UICONTROL Launch Experiences]** wordt geklikt. De eenvoudigste manier is om over te schakelen op een ander scherm en vervolgens terug te keren naar het scherm waar de wijziging naar verwachting zal plaatsvinden.
* Mobiele voorvertoning wordt niet ondersteund voor Android-versies ouder dan API-19 (KitKat).
