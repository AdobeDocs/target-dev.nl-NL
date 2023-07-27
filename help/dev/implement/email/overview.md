---
keywords: Implementatie, at.js non javascript, adbox, redirector, mbox
description: Leer hoe u implementeert [!DNL Adobe Target] in niet-JavaScript-scenario's, zoals het gebruik van een AdBox of Redirector.
title: Hoe implementeren [!DNL Target] voor e-mail?
feature: Implement Email
exl-id: dda00b75-5d58-4405-ae58-75e7883a30ed
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# E-mail: implementeren [!DNL Target]

Informatie over de uitvoering [!DNL Target] in niet-JavaScript-scenario&#39;s, zoals het gebruik van een AdBox of Redirector.

U kunt bezoeken aan advertenties en andere content buiten de site volgen. U kunt dezelfde gebruiker ook op en buiten uw site identificeren en een consistente ervaring bieden tijdens de hele webervaring. Met behulp van één URL staat AdBox tests toe zonder JavaScript of at.js.

Een AdBox is nuttig voor sites die at.js niet hebben, zoals filialen. Als uw activiteit dynamisch creatief (bijvoorbeeld, moet u een product in de advertentie tonen die in het karretje werd verlaten) vereist, kunt u geen AdBox gebruiken.

Advertentievakken en Redirector kunnen met om het even welke soort activiteit worden gebruikt. In de volgende tabel worden ADBox en Redirector vergeleken en wanneer beide worden gebruikt:

| | Doel | Wanneer gebruiken | URL-structuur | Type voorstel | Inhoud voorstellen |
|--- |--- |--- |--- |--- |--- |
| AdBox | Hiermee worden verschillende afbeeldingen naar de advertentie geretourneerd | De inhoud van een advertentie wijzigen | `clientcode&#x200B;.tt.&#x200B;omtrdc&#x200B;.net/&#x200B;m2&#x200B;/&#x200B;clientcode/ubox/&#x200B;image?` | omleidingsvoorstel | URL voor een afbeelding |
| Redirector | Een bezoeker omleiden naar een andere webpagina | De landingspagina van een advertentie wijzigen | `clientcode&#x200B;.tt.omtrdc.net/&#x200B;m2/clientcode&#x200B;/ubox/page?` | omleidingsvoorstel | URL voor een pagina |

## Aanbevolen werkwijzen voor beveiliging

Merk op dat met Redirector, u aan een risico van Open Redirect Kwetsbaarheid kunt worden blootgesteld. Om het ongeoorloofde gebruik van verbindingen van Redirector door derden te vermijden, adviseren wij u &quot;erkende gastheren&quot;gebruiken om de standaard omleiding URL domeinen te lijsten van gewenste personen. [!DNL Target] gebruikt gastheren aan lijst van gewenste personen domeinen waaraan u redirects wilt toestaan. Zie voor meer informatie [Creeer Lijsten van gewenste personen die gastheren specificeren die worden gemachtigd om mbox vraag te verzenden naar [!DNL Target]](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html#allowlist) in *Gastheren*.

## Restricties

* Er is geen time-out aan de clientzijde, net als bij standaardvakken. Indien [!DNL Target] is volledig omlaag, zien bezoekers van de advertentie de inhoud niet, zelfs niet standaard.
* Cookies van derden worden gebruikt om de bezoeken bij te houden. Als de PCIds verschillend zijn, door gebrek wordt de derde partij van de bezoeker samengevoegd met om het even welke bestaande 1st-partijprofielen.
* Als u cookies van de eerste partij op de AdBox zelf wilt gebruiken, moet u de mBox-sessie in de URL doorgeven. Bespreek dit met uw accountvertegenwoordiger.
* Als u cookies van de eerste partij wilt gebruiken om cookies bij te houden en te klikken, geeft u de box-sessie door in de URL. Bespreek dit met uw accountvertegenwoordiger.
* Als u meerdere AdBox op dezelfde pagina wilt gebruiken, moet u de Mbox-sessie doorgeven in de URL. Bespreek dit met uw accountvertegenwoordiger. U hebt mogelijk één AdBox en één Redirector-koppeling op dezelfde pagina (omdat Redirector zich op een tweede pagina bevindt).
