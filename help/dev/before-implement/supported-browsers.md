---
keywords: Browsers, vereisten, vereisten, internetverkenner, chroom, firefox, safari, android, oppervlak, browsers0
description: Meer informatie over browsers op internet [!DNL Adobe Target] ondersteunt de interface en de levering van inhoud.
title: Wat browsers doen [!DNL Target] Ondersteuning?
feature: Implementation
exl-id: 1d778e14-26b0-477b-ac28-d304db70a133
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Ondersteunde browsers

De [!DNL Adobe Target] de toepassing en de inhoudslevering zijn getest in een groot aantal browsers en apparaten.

Voor meer belangrijke informatie over TLS raadpleegt u [De Veranderingen van de Encryptie van TLS (de Veiligheid van de Laag van het Vervoer)](tls-transport-layer-security-encryption.md).

## [!DNL Target] Standaard/Premium-interface

De [!DNL Target] interface ondersteunt de volgende browsers en apparaten:

| Apparaattype | Browserversie |
|--- |--- |
| Windows | <ul><li>Microsoft Edge</li><li>Google Chrome (laatste, laatste min 1)</li><li>Mozilla Firefox (laatste, laatste min 1)</li></ul> |
| Mac | <ul><li>Firefox (laatste, laatste min 1)</li><li>Chrome (nieuwste, laatste min 1)</li></ul> |

## Inhoud leveren

De levering van inhoud is getest in de volgende browsers en apparaten:

| Apparaattype | Browserversie |
|--- |--- |
| Windows | <ul><li>Microsoft Internet Explorer 9 en 10. Getest in emulatiemodus. **Opmerking**: De levering van inhoud op IE 9 wordt niet meer ondersteund met at.js 1.3.0 (en hoger). De levering van inhoud op IE 10, 11, en alle oudere versies wordt niet meer gesteund met at.js 2.5.0 (en later).</li><li>Internet Explorer 11. **Opmerking**: De levering van inhoud op IE 10, 11 en alle oudere versies wordt niet meer ondersteund met at.js 2.5.0 (en hoger).</li><li>Microsoft Edge</li><li>Chrome (nieuwste, laatste min 1)</li><li>Firefox (laatste, laatste min 1)</li></ul> |
| Mac | <ul><li>Apple Safari (nieuwste). **Opmerking**: Voor meer informatie over hoe Safari cookies van eerste en van derde partijen verwerkt, raadpleegt u [Doelcookie](../implement/client-side/atjs/atjs-cookies.md).</li><li>Firefox (laatste, laatste min 1)</li><li>Chrome (nieuwste, laatste min 1)</li></ul> |
| Mobiel/tablet | <ul><li>Apple iOS (nieuwste)</li><li>Android-apparaten en -tablets (Android 4 en hoger)</li><li>Microsoft-oppervlak (Windows 8.1)</li></ul> |

Let op het volgende:

* Voor implementaties van at.js, [!DNL Target] Hiermee geeft u standaardinhoud weer in eerdere versies van Internet Explorer en mogelijk in eerdere versies van de hierboven vermelde browsers.
* Internet Explorer behandelt alle onbekende elementen (zoals aangepaste elementen) als hetzelfde elementtype. Dientengevolge, werkt de levering niet met douaneelementen.
* [!DNL Target] geeft standaardinhoud weer in browsers die hierboven niet worden vermeld en in browsers die [quirks, modus](https://en.wikipedia.org/wiki/Quirks_mode). at.js vereist een documenttype dat op standaardwijze teruggeeft, bijvoorbeeld: `<!DOCTYPE html>` .
* [!DNL Adobe] Leveringsinfrastructuur wordt na 12 september 2018 beveiligd om GEEN TLS 1.0-apparaten en browsers te ondersteunen. Zie [De Veranderingen van de Encryptie van TLS (de Veiligheid van de Laag van het Vervoer)](../before-implement/tls-transport-layer-security-encryption.md) inzicht te krijgen in de algemene gevolgen van deze wijziging.
