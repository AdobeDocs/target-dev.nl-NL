---
keywords: inhoudsbeveiligingsbeleid, csp, at.js, whitelist, lijst van gewenste personen, flikkering, voorverbergen, voorverbergen, voorverbergen, inhoudsbeveiligingsbeleid, iFrame, iframe
description: Meer informatie over de CSP-instructies (Content Security Policy) die u moet toevoegen bij het gebruik van [!DNL Adobe Target].
title: Hoe werkt [!DNL Target] Beveiligingsbeleid voor inhoud (CSP) verwerken?
feature: Privacy & Security
exl-id: ec6942e5-36d8-4f88-b3d6-47f9eaca03a8
source-git-commit: c43c79b29768694eac534e22047b5ee6a3d0ccd5
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# Inhoudsbeveiligingsbeleid (CSP)-instructies

Als u het [Beveiligingsbeleid voor inhoud](https://en.wikipedia.org/wiki/Content_Security_Policy) (CSP) voor uw [!DNL Adobe Target] implementatie, moet u de volgende CSP-instructies toevoegen bij het gebruik [at.js 2.1 of hoger](../../implement/client-side/atjs/target-atjs-versions.md):

* `connect-src` with `*.tt.omtrdc.net` gevoegd op lijst van gewenste personen. Noodzakelijk om het netwerkverzoek toe te staan aan [!DNL Target] rand.
* `style-src unsafe-inline`. Vereist voor het voorbeverbergen en flikkeren van de besturing.
* `script-src unsafe-inline`. Vereist om JavaScript-uitvoering toe te staan die deel kan uitmaken van een HTML-aanbieding.

## Veelgestelde vragen

Raadpleeg de volgende veelgestelde vragen over beveiligingsbeleid:

### Zijn de het Delen van Middelen van het Middel van de Oorsprong (CORS) en het beleid van de Flash dwars-domein veiligheidskwesties?

De geadviseerde manier om het beleid van CORS uit te voeren is toegang tot slechts vertrouwde op oorsprong toe te staan die het via een lijst van gewenste personen van vertrouwde op domeinen vereisen. Hetzelfde kan gezegd worden van het Flash-interdomeinbeleid. Sommige [!DNL Target] klanten maken zich zorgen over het gebruik van jokertekens voor domeinen in Target. De zorg is dat als een gebruiker aan een toepassing het programma wordt geopend, en een domein bezoekt dat door het beleid wordt toegestaan, om het even welke kwaadwillige inhoud die op dat domein loopt gevoelige inhoud van de toepassing kan terugwinnen en acties binnen de veiligheidscontext van de het programma geopende gebruiker uitvoeren. Deze situatie wordt algemeen bedoeld als Cross-Site Request vervalsing (CSRF).

In een [!DNL Target] de uitvoering van dit beleid mag echter geen veiligheidskwestie zijn .

&quot;adobe.tt.omtrdc.net&quot; is een domein dat eigendom is van Adobe. [!DNL Adobe Target] is een test- en personalisatiehulpmiddel en verwacht wordt dat [!DNL Target] kan verzoeken van overal ontvangen en verwerken zonder enige authentificatie te vereisen. Deze verzoeken bevatten sleutel/waardeparen die voor het testen A/B, aanbevelingen, of inhoudspartnerij worden gebruikt.

Adobe slaat geen PII (Personal Identified Information) of andere gevoelige informatie op [!DNL Adobe Target] Edge-servers, waarnaar &quot;adobe.tt.omtrdc.net&quot; wijst.

Verwacht wordt dat [!DNL Target] vanuit elk domein toegankelijk zijn via JavaScript-aanroepen. De enige manier om deze toegang toe te staan is door &quot;toegang-controle-toe:staan-Oorsprong&quot;met een vervanging toe te passen.

### Hoe kan ik toestaan of voorkomen dat mijn site wordt ingesloten als een iFrame onder externe domeinen?

Om de [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank} (VEC) Als u uw website wilt insluiten in een iFrame, moet de CSP (indien ingesteld) worden gewijzigd in de instelling van de webserver. [!DNL Adobe] domeinen moeten worden gewhitelisteerd en geconfigureerd.

Om veiligheidsredenen is het wellicht verstandig om te voorkomen dat uw site wordt ingesloten als een iFrame onder externe domeinen.

In de volgende secties wordt uitgelegd hoe u het insluiten van uw site in een iFrame door de VEC toestaat of voorkomt.

#### VEC toestaan uw site in te sluiten in een iFrame

De eenvoudigste oplossing om VEC in te schakelen voor het insluiten van uw website in een iFrame is om `*.adobe.com`, wat het breedste jokerteken is.

Bijvoorbeeld:

`Content-Security-Policy: frame-ancestors 'self' *.adobe.com`

Zoals in de volgende afbeelding (klik om te vergroten):


![CSP met breedste vervanging](/help/dev/before-implement/privacy/assets/csp-adobe.png){width="600" zoomable="yes"}

Mogelijk wilt u alleen het daadwerkelijke [!DNL Adobe] service. Dit scenario kan worden bereikt door `*.experiencecloud.adobe.com + https://experiencecloud.adobe.com`.

Bijvoorbeeld:

`Content-Security-Policy: frame-ancestors 'self' https://*.experiencecloud.adobe.com https://experiencecloud.adobe.com https://experience.adobe.com`

Zoals in de volgende afbeelding (klik om te vergroten):

![CSP met ExperienceCloud-bereik](/help/dev/before-implement/privacy/assets/csp-experiencecloud.png){width="600" zoomable="yes"}

De meest restrictieve toegang tot de rekening van een onderneming kan worden bereikt door `https://<Client Code>.experiencecloud.adobe.com https://experience.adobe.com`, waarbij `<Client Code>` vertegenwoordigt uw specifieke cliëntcode.

Bijvoorbeeld:

`Content-Security-Policy: frame-ancestors 'self'  https://ags118.experiencecloud.adobe.com https://experience.adobe.com`

Zoals in de volgende afbeelding (klik om te vergroten):

![CSP met clientcode waarop het bereik van toepassing is](/help/dev/before-implement/privacy/assets/csp-clientcode.png){width="600" zoomable="yes"}

>[!NOTE]
>
>Als u [Starten/Tag](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) en moet ook worden ontgrendeld.
>
>Bijvoorbeeld:
>
> `Content-Security-Policy: frame-ancestors 'self' *.adobe.com *.assets.adobedtm.com;`

#### Voorkomen dat de VEC uw site insluit in een iFrame

Als u wilt voorkomen dat de VEC uw site insluit in een iFrame, kunt u zich beperken tot alleen &quot;zelf&quot;.

Bijvoorbeeld:

`Content-Security-Policy: frame-ancestors 'self'`

Zoals getoond in de volgende afbeelding (klik om te vergroten):

![CSP-fout](/help/dev/before-implement/privacy/assets/csp-error.png){width="600" zoomable="yes"}

Het volgende foutbericht wordt weergegeven:

`Refused to frame 'https://kuehl.local/' because an ancestor violates the following Content Security Policy directive: "frame-ancestors 'self'".`

