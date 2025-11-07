---
keywords: appel, ITP, intelligente traceringspreventie, ervaring cloud id, ecid, itp
description: Leer over  [!DNL Adobe Target]  en het effect van het initiatief van de Preventie van het Intelligente Volgen van Apple (ITP) dat probeert om de privacy van gebruikers van Safari te beschermen.
title: Hoe behandelt  [!DNL Target]  de Steun van Apple ITP?
feature: Privacy & Security
exl-id: 6deee03b-df86-4d0d-999c-b11855ddfda5
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# Apple Intelligent Tracking Prevention (ITP) 2.x

Intelligent Tracking Prevention (ITP) is een Apple-initiatief om de privacy van Safari-gebruikers te beschermen. De eerste release van ITP, die in 2017 plaatsvond, was gericht op het gebruik van cookies van derden. Apple heeft namelijk alle cookies van derden geblokkeerd, wat op zijn beurt weer ernstige hoofdpijn heeft veroorzaakt voor technische en technische bedrijven, omdat cookies van derden over het algemeen worden gebruikt voor het bijhouden van bezoekers en het verzamelen van bezoekersgegevens. Apple is nu op weg om beperkingen en beperkingen in te stellen voor het gebruik van cookies van eerste partijen in Safari.

Deze versies van ITP bevatten de volgende beperkingen:

| Versie | Details |
| --- | --- |
| [&#x200B; ITP 2.1 &#x200B;](https://webkit.org/blog/8613/intelligent-tracking-prevention-2-1/) | Er zijn maximaal zeven dagen verstreken voordat de cookies aan de clientzijde die met de API `document.cookie` op de browser worden geplaatst.<br /> vrijgegeven 21 februari 2019. |
| [&#x200B; ITP 2.2 &#x200B;](https://webkit.org/blog/8828/intelligent-tracking-prevention-2-2/) | Verminderde de 7-daagse vervalsingsdop drastisch tot één dag.<br /> vrijgegeven 24 april 2019. |
| [&#x200B; ITP 2.3 &#x200B;](https://webkit.org/blog/9521/intelligent-tracking-prevention-2-3/) | Er zijn verschillende obstakels verwijderd, zoals het gebruik van localStorage of het gebruik van de JavaScript `Document.referrer property` .<br /> vrijgegeven 23 september 2019.<br /> CNAME-camouflage defensie eigenschap aan ITP die in Safari 14, macOS Big Sur, Catalina, Mojave, iOS 14, en iPad OS 14 wordt vrijgegeven. Alle cookies die door een derde CNAME-camouflage HTTP-respons worden gemaakt, verlopen over zeven dagen.<br /> kondigde 12 november 2020 aan. |

## Wat is de impact voor mij als [!DNL Target] klant?

Doel biedt JavaScript-bibliotheken die u op uw pagina&#39;s kunt gebruiken, zodat [!DNL Target] uw bezoekers in real-time een persoonlijk tintje kan geven. Er zijn drie [!DNL Target] JavaScript-bibliotheken op 1.js.*x*, at.js 2.*x*, [!DNL Adobe Experience Cloud Web SDK] die cliënt-kant [!DNL Target] koekjes op browsers van uw bezoekers via `document.cookie` API plaatsen. Als gevolg hiervan worden cookies van [!DNL Target] beïnvloed door Apple ITP 2.1, 2.2 en 2.3 en verlopen deze na zeven dagen (met ITP 2.1) en na één dag (met ITP 2.2 en ITP 2.3).

Apple ITP 2.x beïnvloedt [!DNL Target] op de volgende gebieden:

| Gevolgen | Details |
| --- | --- |
| Mogelijke toename van het aantal unieke bezoekers | Omdat het afloopvenster wordt ingesteld op zeven dagen (met ITP 2.1) en één dag (met ITP 2.2 en ITP 2.3), kan het zijn dat er een toename is van unieke bezoekers die uit Safari-browsers komen. Als uw bezoekers uw domein na zeven dagen (ITP 2.1) of één dag (ITP 2.2 en ITP 2.3) terugkeren, wordt [!DNL Target] gedwongen om een nieuwe [!DNL Target] cookie op uw domein te plaatsen in plaats van de verlopen cookie. Het nieuwe [!DNL Target] cookie wordt omgezet naar een nieuwe unieke bezoeker, ook al is de gebruiker hetzelfde. |
| Verlaagde terugzoektijden voor [!DNL Target] activiteiten | Bezoekersprofielen voor [!DNL Target] -activiteiten hebben mogelijk een kortere terugzoekperiode voor beslissingen. [!DNL Target] cookies worden gebruikt om een bezoeker te identificeren en gebruikersprofielkenmerken op te slaan voor personalisatie. Aangezien [!DNL Target] -cookies na zeven dagen (ITP 2.1) of één dag (ITP 2.2 en 2.3) in Safari kunnen verlopen, kunnen de gebruikersprofielgegevens die aan het gezuiverde [!DNL Target] -cookie waren gekoppeld, niet worden gebruikt voor beslissingen. |
| Profielscripts gebaseerd op 3rdPartyID | Wegens het vervalvenster dat aan zeven dagen (met ITP 2.1) en één dag (met ITP 2.2 en ITP 2.3) wordt geplaatst, [&#x200B; profielmanuscripten &#x200B;](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html) die op het cookie 3rdPartyID worden gebaseerd zullen ophouden werkend bij afloop. |
| URL&#39;s met kwaliteitscontrole/voorvertoning op iOS-apparaten | Wegens het vervalvenster dat aan zeven dagen (met ITP 2.1) en één dag (met ITP 2.2 en ITP 2.3) wordt geplaatst, [&#x200B; QA/Voorproef URLs &#x200B;](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) zal ophouden werkend bij afloop omdat URLs op het cookie 3rdPartyID gebaseerd is. |

## Heeft dit gevolgen voor mijn huidige implementatie van [!DNL Target] ?

Als u de bibliotheek van Experience Cloud identiteitskaart (ECID) naast de [!DNL Target] bibliotheek van JavaScript gebruikt, zal uw implementatie op de manieren worden beïnvloed die in dit artikel worden vermeld: [&#x200B; Safari ITP 2.1 Effect op de Klanten van Adobe Experience Cloud en van Experience Platform &#x200B;](https://medium.com/adobetech/safari-itp-2-1-impact-on-adobe-experience-cloud-customers-9439cecb55ac).
