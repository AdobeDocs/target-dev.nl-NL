---
keywords: aanbieding, prefetch, iOS, android, sdk, mobile, mobile SDK, $ 8
description: Gebruik de [!DNL Adobe Target] Prefetch-functie in de SDK's van iOS en Android Mobile om inhoud van aanbiedingen zo weinig mogelijk op te halen door de serverreacties in cache te plaatsen.
title: Kan ik inhoud voor mobiele apps vooraf aanbieden?
feature: Implement Mobile
exl-id: 6f8e8298-f1e9-46f0-828f-717c7d632077
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# Prefetaanbiedingsinhoud

De [!DNL Target] De prefetch-functie gebruikt de SDK&#39;s van iOS en Android Mobile om inhoud van de aanbieding zo weinig mogelijk op te halen door de serverreacties in cache te plaatsen.

>[!IMPORTANT]
>
>Steun voor de [!DNL Adobe Mobile] versie 4.*x* SDK&#39;s zijn geëindigd op 31 augustus 2021 en worden niet langer aanbevolen voor [!DNL Adobe Target] mobiele gebruikers.
>
>De [Adobe Experience Platform SDK voor mobiele apps](https://developer.adobe.com/client-sdks/documentation/){target=_blank} is de aanbevolen oplossing voor stroom [!DNL Adobe Experience Cloud] oplossingen en services in uw mobiele apps.

Dit proces verkort de ladingstijd, verhindert veelvoudige netwerkvraag, en staat toe [!DNL Target] om op de hoogte te worden gebracht van de mbox die door de gebruiker van de mobiele app is bezocht. Alle inhoud wordt teruggewonnen en in het voorgeheugen ondergebracht tijdens de prefetch vraag, en deze inhoud wordt teruggewonnen van het geheime voorgeheugen voor alle toekomstige vraag die caching inhoud voor de gespecificeerde mbox naam bevat.

Houd rekening met de volgende beperkingen wanneer u de prefetch-methode gebruikt met de iOS en Android Mobile SDK&#39;s:

* Prefetch-inhoud blijft niet behouden bij alle opstarters. De prefetch-inhoud wordt in de cache geplaatst zolang de toepassing actief is of totdat de `clearPrefetchCache()` wordt aangeroepen.
* Prefetch-functionaliteit wordt niet ondersteund voor [!UICONTROL Auto-Allocate] en [!UICONTROL Auto-Target] verkeerstoewijzingsmethoden, voor [!UICONTROL Automated Personalization] of [!UICONTROL Recommendations] typen activiteit, of voor [aanbevelingen worden aangeboden binnen een A/B- of XT-activiteit](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-as-an-offer.html?lang=nl-NL).

Voor meer informatie, met inbegrip van prefetch methodes, openbare klassen, en codesteekproeven, zie:

* **iOS:**  [Prefetch-aanbiedingsinhoud in iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/target-ios/c-mob-target-prefetch-ios.html?lang=nl-NL) in de *Help bij Mobile Services iOS SDK*.
* **Android:**  [Inhoud van Prefetch-aanbieding in Android](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html) in de *Help bij Mobile Services Android SDK*.
