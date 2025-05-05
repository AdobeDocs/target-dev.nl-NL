---
keywords: implementeren, implementeren, instellen, instellen, paginaparameter
description: Gegevens ophalen in [!DNL Target] gebruiken van profielkenmerken in de pagina.
title: Hoe krijg ik gegevens in [!DNL Target] Profielkenmerken in pagina gebruiken?
feature: Implementation
exl-id: c19fd746-21a2-4eb5-8c2a-c24806e09324
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# Profielkenmerken in pagina

Profielkenmerken in pagina [!DNL Adobe Target] (ook wel &#39;in-mbox-profielkenmerken&#39; genoemd) zijn naam-/waardeparen die rechtstreeks via paginacode worden doorgegeven en die in het profiel van de bezoeker worden opgeslagen voor toekomstig gebruik.

Met profielkenmerken van pagina&#39;s kunnen gebruikersspecifieke gegevens in het doelprofiel worden opgeslagen, zodat deze later kunnen worden toegewezen en gesegmenteerd.

## Indeling

Profielkenmerken in de pagina worden doorgegeven aan [!DNL Target] via een serveraanroep als een naam/waardepaar met het voorvoegsel &quot;profiel&quot;. vóór de kenmerknaam.

Kenmerknamen en -waarden kunnen worden aangepast (hoewel er enkele &#39;gereserveerde namen&#39; zijn voor specifieke toepassingen).

Hier volgen enkele voorbeelden van kenmerken van profielen in pagina&#39;s:

* `profile.membershipLevel=silver`
* `profile.visitCount=3`

## Voorbeelden van gebruiksgevallen

* **Aanmeldingsgegevens**: Deel niet-PII-gegevens (Persoonlijk identificeerbare informatie) naar [!DNL Target] op basis van de gebruikersaanmelding. Dit kunnen lidmaatschapsstatus, ordergeschiedenis of meer zijn.
* **Winkelinfo**: Volg welke winkel de voorkeurslocatie van deze gebruiker is.
* **Vorige interacties**: Volg wat de gebruiker eerder op de site heeft gedaan om toekomstige personalisatie te informeren.

## Voordelen van de methode

Gegevens die worden verzonden naar [!DNL Target] in real time, en kan op de zelfde servervraag worden gebruikt waarop de gegevens binnen komen.

## Caveats

Vereist updates van paginacode (direct of via een systeem voor tagbeheer).

Kenmerken en waarden zijn zichtbaar in serveraanroepen, zodat een bezoeker de waarden kan zien. Als het delen van informatie zoals kredietbereiken of andere potentieel particuliere informatie, zou deze methode niet de beste benadering kunnen zijn.

## Codevoorbeelden

targetPageParamsAll (voegt de attributen aan alle mbox vraag op de pagina toe):

`function targetPageParamsAll() { return "profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

targetPageParams (voegt de kenmerken toe aan het globale mabox op de pagina):

`function targetPageParams() { return profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

Kenmerken in mboxCreate-code:

`<div class="mboxDefault"> default content to replace by offer </div> <script> mboxCreate('mboxName','profile.param1=value1','profile.param2=value2'); </script>`

## Koppelingen naar relevante informatie

[Profielkenmerken](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=nl-NL)

[Bezoekerprofiel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=nl-NL)
