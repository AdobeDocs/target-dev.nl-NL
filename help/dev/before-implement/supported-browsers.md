---
keywords: Browsers, vereisten, vereisten, internetverkenner, chroom, firefox, safari, android, oppervlak, browsers0
description: Leer welke Internet browsers  [!DNL Adobe Target]  voor zijn interface en voor inhoudslevering steunt.
title: Welke browsers steunt  [!DNL Target] ?
feature: Implementation
exl-id: 1d778e14-26b0-477b-ac28-d304db70a133
source-git-commit: 1b6dcb24d677b758ed1daf85dc0a7e9e5b42680d
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Ondersteunde browsers

De toepassing van [!DNL Adobe Target] en de levering van inhoud zijn getest voor een groot aantal browsers en apparaten.

Voor meer belangrijke informatie over TLS, zie [&#x200B; de Veranderingen van de Encryptie van TLS (de Veiligheid van de Laag van het Vervoer) &#x200B;](tls-transport-layer-security-encryption.md).

## [!DNL Target] Standard/Premium-interface

De interface [!DNL Target] ondersteunt de volgende browsers en apparaten:

>[!NOTE]
>
>Doel ondersteunt de nieuwste versie van elke weergegeven browser en de nieuwste versie min 1.


| Apparaattype | Browserversie |
|--- |--- |
| [!DNL Windows] | <ul><li>[!DNL Microsoft Edge]</li><li>[!DNL Google Chrome]</li><li>[!DNL Mozilla Firefox]</li></ul> |
| [!DNL Mac] | <ul><li>[!DNL Microsoft Edge]</li><li>[!DNL Google Chrome]</li><li>[!DNL Mozilla Firefox]</li></ul> |

## Vereisten voor visuele bewerking

Om uw Web-pagina&#39;s in [!UICONTROL Visual Experience Composer] (VEC) betrouwbaar te kunnen openen, auteur, en voorproef, moet u de [&#x200B; Adobe Experience Cloud Visuele het Uitgeven browser van de Helper browser van de Helper &#x200B;](https://experienceleague.adobe.com/nl/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension){target=_blank}  hebben die op uw Webbrowser of gebruik [!UICONTROL Enhanced Experience Composer (EEC)] wordt geïnstalleerd.

>[!NOTE]
>
>[!DNL Google Chrome] en [!DNL Microsoft Edge] zijn momenteel de enige browsers die visuele bewerking van webpagina&#39;s in [!DNL Adobe Target] ondersteunen.


## Inhoud leveren

De levering van inhoud is getest in de volgende browsers en apparaten:

| Apparaattype | Browserversie |
|--- |--- |
| Windows | <ul><li>Microsoft Internet Explorer 9 en 10. Getest in emulatiemodus. **Nota**: De levering van de inhoud op IE 9 wordt niet meer gesteund met at.js 1.3.0 (en later). De levering van inhoud op IE 10, 11, en alle oudere versies wordt niet meer gesteund met at.js 2.5.0 (en later).</li><li>Internet Explorer 11. **Nota**: De levering van de inhoud op IE 10, 11, en alle oudere versies wordt niet meer gesteund met at.js 2.5.0 (en later).</li><li>Microsoft Edge</li><li>Chrome (laatste, laatste min 1)</li><li>Firefox (laatste, laatste min 1)</li></ul> |
| Mac | <ul><li>Apple Safari (nieuwste). **Nota**: Voor meer informatie over hoe de handvatten Safari eerste en derdekoekjes, [&#x200B; Koekje van het Doel &#x200B;](../implement/client-side/atjs/atjs-cookies.md) zien.</li><li>Firefox (laatste, laatste min 1)</li><li>Chrome (laatste, laatste min 1)</li></ul> |
| Mobiel/tablet | <ul><li>Apple iOS (nieuwste)</li><li>Android devices en tablets (Android 4 en hoger)</li><li>Microsoft-oppervlak (Windows 8.1)</li></ul> |

Let op het volgende:

* [!DNL Adobe Experience Platform Web SDK] is ontworpen om optimaal te werken in de nieuwste versies van [!DNL Google Chrome] , [!DNL Safari] , [!DNL Firefox] en [!DNL Microsoft Edge Chromium] . Mogelijk kunt u problemen ondervinden bij het gebruik van bepaalde functies in oudere versies van deze browsers of afgekeurde browsers, zoals [!DNL Internet Explorer] .
* Voor at.js-implementaties geeft [!DNL Target] standaardinhoud weer in eerdere versies van Internet Explorer en mogelijk in eerdere versies van de hierboven vermelde browsers.
* Internet Explorer behandelt alle onbekende elementen (zoals aangepaste elementen) als hetzelfde elementtype. Dientengevolge, werkt de levering niet met douaneelementen.
* [!DNL Target] vertoningen standaardinhoud in browsers hierboven niet vermeld en in browsers gebruikend [&#x200B; kronkelwijze &#x200B;](https://en.wikipedia.org/wiki/Quirks_mode). at.js vereist een documenttype dat in de standaardmodus wordt weergegeven, bijvoorbeeld: `<!DOCTYPE html>` .
* [!DNL Adobe] Leveringsinfrastructuur wordt na 12 september 2018 beveiligd voor NIET-ondersteuning van TLS 1.0-apparaten en browsers. Zie [&#x200B; TLS (de Veiligheid van de Laag van het Vervoer) de Veranderingen van de Encryptie &#x200B;](../before-implement/tls-transport-layer-security-encryption.md) om het algemene effect van deze verandering te begrijpen.
