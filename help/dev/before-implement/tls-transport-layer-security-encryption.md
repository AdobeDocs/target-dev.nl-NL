---
keywords: tls, tls 1.0, de veiligheid van de vervoerlaag, encryptie, tls 1.1, tls 1.2
description: Meer informatie [!DNL Target] gebruikt het protocol van TLS (de Veiligheid van de Laag van het Vervoer) om de hoogste veiligheidsnormen te handhaven en de veiligheid van uw klantengegevens te bevorderen.
title: Hoe werkt [!DNL Target] TLS gebruiken om beveiliging te bieden?
feature: Privacy & Security
exl-id: f5ea2272-27ab-49c9-b096-b15dd277d4e5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 0%

---

# TLS (Transport Layer Security)-coderingswijzigingen

Informatie over hoe [!DNL Adobe] en [!DNL Adobe Target] gebruik TLS (Transport Layer Security) om de hoogste beveiligingsnormen te handhaven en de veiligheid van klantgegevens te bevorderen.

De Veiligheid van de Laag van het vervoer (TLS) is het wijdst opgestelde veiligheidsprotocol dat vandaag voor Webbrowsers en andere toepassingen wordt gebruikt die gegevens vereisen om veilig over een netwerk worden geruild. Adobe beschikt over normen voor beveiligingscompatibiliteit die het einde van de levensduur van oudere protocollen vereisen en die het gebruik van TLS 1.2 verplicht stellen om de meest actuele en veilige versie in gebruik te hebben.

>[!WARNING]
>
>Vanaf 1 maart 2020, [!DNL Target] biedt geen ondersteuning meer voor TLS 1.1-codering voor Visual Experience Composer (VEC), Enhanced Experience Composer (EEC), levering van activiteiten, API&#39;s, enz. Voer een upgrade uit naar TLS 1.2 om problemen te voorkomen.

We verwachten niet dat dit een aanzienlijke invloed zal hebben op klantgegevens of rapportage.

## Visual Experience Composer (VEC) met Enhanced Experience Composer (EEC) Enabled

TLS 1.2 is de standaard vanaf 1 maart 2020 en TLS 1.1 wordt niet meer ondersteund.

Adobe verplaatst klanten geleidelijk naar TLS 1.2. Voor degenen, wier domeinen reeds 1.2 volgzaam zijn, zullen wij hen naar TLS 1.2 zonder enige veranderingen verplaatsen nodig van u. De meeste klantdomeinen ondersteunen al TLS 1.2. Als uw domein echter geen TLS 1.2 ondersteunt, behouden we deze domeinen op TLS 1.1 zoals vandaag (tot maart 2020).

Tijdens deze migratiefase mag u geen enkel probleem tegenkomen. Als de VEC is gestopt met het laden van een site die eerder werkte, [een Client Care-ticket openen](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?lang=nl-NL&#reference_ACA3391A00EF467B87930A450050077C) deze migratie als mogelijke oorzaak aanvoeren.

Als u echter een van deze klanten bent die op TSL 1.1 werken zonder TLS 1.2 te ondersteunen, moet u plannen voor het verplaatsen van uw domeinen/infrastructuur naar TLS 1.2. We zullen het TLS 1.1-protocol blijven ondersteunen tot 1 maart 2020. Vanaf 1 maart 2020, [!DNL Target] biedt geen ondersteuning voor het TLS 1.1-protocol dat via de Enhanced Experience Composer-functie voor de VEC moet worden gebruikt.

Hoewel wij iedereen ten zeerste adviseren om op TLS 1.2 vooruit te zijn, als u een nieuwe klant bent maar *NOT* ondersteuning biedt voor TLS 1.2, neemt u contact op met de klantenservice om hen te informeren dat u TLS 1.1 moet gebruiken voor de Enhanced Experience Composer. Overstappen naar TLS 1.2 is echter niet mogelijk, aangezien u ook na 1 maart 2020 geen ondersteuning meer krijgt.

## Levering van activiteiten

Vanaf 1 maart 2020, [!DNL Target] -servers ondersteunen TLS 1.1 niet meer. Met deze wijziging [!DNL Target] -servers accepteren geen aanvragen meer van bezoekers met oudere apparaten of webbrowsers die geen TLS 1.2 (of hoger) ondersteunen. Hierdoor ontvangen oudere apparaten en browsers die alleen TLS 1.1 ondersteunen (of standaard TLS 1.1 ondersteunen) geen inhoud met activiteiten van Adobe Target. De standaardinhoud van de site wordt weergegeven.

Tot de oudere apparaten en browsers die worden beïnvloed behoren:

* Google Chrome (Chrome voor Android) versie 29 en lager
* Opera Browser (Opera Mobile) versie 12.17 en eerdere versies
* Mozilla Firefox (Firefox voor mobiele apparaten) versie 26 en lager
* Android 4.3 en eerdere versies
* Internet Explorer 8-10 in Windows 7 en eerdere versies
* Internet Explorer 10 op Windows Phone 8.0
* Safari 6.0.4/OS X10.8.4 en eerdere versies

Overweeg het volgende terwijl u deze wijziging wilt uitvoeren (de deadline van 1 maart 2020 beïnvloedt al deze items):

* U moet ervoor zorgen dat uw standaardsite gereed is op een manier die geschikt is voor compatibele apparaten en browsers.
* Houd er rekening mee dat het aantal bezoekers in uw [!DNL Target] in rapporten kan een onbeduidende daling van het aantal bezoekers worden waargenomen .
* Mogelijk moet u het publiek wijzigen dat specifiek is gemaakt voor oudere apparaten of browsers die geen TLS 1.2 ondersteunen. Levering aan deze apparaten en browsers werkt niet meer.

Voor meer informatie over ondersteunde browsers en hun versies raadpleegt u [Ondersteunde browsers](supported-browsers.md).

## [!DNL Adobe Target] API&#39;s

Vanaf 1 maart 2020, [!DNL Target] API&#39;s ondersteunen geen TLS 1.1-codering meer. Klanten die toegang hebben tot de API moeten controleren of dit geen gevolgen heeft.

* API-clients die Java 7 met standaardinstellingen gebruiken, moeten worden gewijzigd om TLS 1.2 te ondersteunen. Zie voor meer informatie &quot; [Standaardversie van TLS-protocol voor eindpunten van client wijzigen: TLS 1.0 in TLS 1.2](https://www.java.com/en/configure_crypto.html)&quot; op de Java-website.
* API-clients die Java 8 gebruiken, moeten niet worden beïnvloed omdat de standaardinstelling TLS 1.2 is.
* API-clients die andere frameworks gebruiken, moeten contact opnemen met hun leveranciers voor meer informatie over TLS 1.2-ondersteuning.

## Toegang tot Experience Cloud Solutions-interfaces

Omdat de [!DNL Target] Standaard/Premium-interface vereist al een [moderne webbrowser](supported-browsers.md)We verwachten echter geen problemen. Als u geen verbinding kunt maken met Target, moet u de browser upgraden naar de meest recente versie.

## Controleren welke TLS-versie uw browser gebruikt

U kunt als volgt de TLS-versie op uw website controleren met Google Chrome:

1. Open de desbetreffende website in Chrome.
1. Klik in het menu Chrome (de drie verticale ovalen) op Meer gereedschappen > Gereedschappen voor ontwikkelaars.

   ![Chrome Developer Tools](assets/chrome-developer-tools.png)

1. Open het tabblad Beveiliging en bekijk vervolgens de TLS-versiegegevens onder Verbinding:

   ![TLS-versiedetails](assets/chrome-tls-version.png)

>[!NOTE]
>
>Deze instructies zijn actueel vanaf de publicatie en kunnen worden gewijzigd. Een snelle internetzoekactie moet helpen als deze instructies veranderen. Andere browsers hebben vergelijkbare stappen.

## Verwacht gedrag bij browsers die TLS-versies onder 1.2 ondersteunen

In deze sectie wordt beschreven wat u alleen kunt verwachten bij browsers die TLS-versies onder 1.2 ondersteunen wanneer u een at.js-implementatie gebruikt. Ter vergelijking wordt in deze sectie ook beschreven wat u kunt verwachten bij browsers die TLS 1.2 ondersteunen.

### Centrale eindpunten

| [!DNL Target] JavaScript-implementatie | Details |
|--- |--- |
| at.js | Als TLS 1.0 of TLS 1.1 is ingeschakeld:<ul><li>Gebruikend browser ontwikkelt hulpmiddelen, op het lusje van het Netwerk, zult u &quot;200 O.K.&quot;zien. Dit betekent dat het verzoek is geslaagd.</li><li>De gebruiker ziet een bericht &quot;Kan niet veilig met deze pagina verbinden&quot;. In het bericht wordt uitgelegd dat dit kan worden veroorzaakt omdat de site verouderde of onveilige TLS-beveiligingsinstellingen gebruikt.</li><li>Er worden geen consolefouten weergegeven.</li></ul>Met TLS 1.2 ingeschakeld:<ul><li>bestand at.js wordt gedownload.</li></ul> |

### Eindpunten rand

| [!DNL Target] JavaScript-implementatie | Details |
|--- |--- |
| Adobe Experience Platform Web SDK | Als TLS 1.0 of TLS 1.1 is ingeschakeld:<ul><li>Gebruikend browser ontwikkelt hulpmiddelen, op het lusje van het Netwerk, zult u &quot;200 O.K.&quot;zien. Dit betekent dat het verzoek is geslaagd.</li><li>De gebruiker ziet een bericht &quot;Kan niet veilig met deze pagina verbinden&quot;. In het bericht wordt uitgelegd dat dit kan worden veroorzaakt omdat de site verouderde of onveilige TLS-beveiligingsinstellingen gebruikt.</li><li>Er worden geen consolefouten weergegeven.</li><li>De standaardinhoud wordt weergegeven.</li></ul>Met TLS 1.2 ingeschakeld:<ul><li>Inhoud van voorstel wordt weergegeven.</li></ul> |
| at.js | Als TLS 1.0 of TLS 1.1 is ingeschakeld:<ul><li>Gebruikend browser ontwikkelt hulpmiddelen, op het lusje van het Netwerk, zult u &quot;200 O.K.&quot;zien. Dit betekent dat het verzoek is geslaagd.</li><li>De gebruiker ziet een bericht &quot;Kan niet veilig met deze pagina verbinden&quot;. In het bericht wordt uitgelegd dat dit kan worden veroorzaakt omdat de site verouderde of onveilige TLS-beveiligingsinstellingen gebruikt.</li><li>Er worden geen consolefouten weergegeven.</li><li>De standaardinhoud wordt weergegeven.</li></ul>Met TLS 1.2 ingeschakeld:<ul><li>Inhoud van voorstel wordt weergegeven.</li></ul> |

### Activiteit gericht met browser-versie publiek (Internet Explorer, Versies 6, 7, of 8)

Het publiek werkt niet meer.

| [!DNL Target] JavaScript-implementatie | Details |
|--- |--- |
| Adobe Experience Platform Web SDK | De Platform-SDK wordt niet ondersteund in eerdere versies dan versie 10 van Internet Explorer. |
| at.js | at.js wordt niet ondersteund in versies van Internet Explorer ouder dan versie 10. |
