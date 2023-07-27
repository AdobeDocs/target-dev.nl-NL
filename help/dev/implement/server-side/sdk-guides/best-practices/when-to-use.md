---
source-git-commit: 5c66ee5c8dd5fe60eaeed10fdb9bb6dcee000c89
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---
# Wanneer moet u op het apparaat versus randbeslissingen gebruiken

## Overweeg gebruiksgevallen wanneer u besluit of u apparaatbeslissingen wilt gebruiken

![alternatieve afbeelding](assets/comparison.jpeg)

Het belangrijkste verschil tussen *op apparaat* Besluiten en randbeslissingen zijn dat beslissingen op het apparaat lokaal op uw servers worden uitgevoerd, terwijl beslissingen over Edge-servers op het Adobe Target Edge-netwerk worden genomen. Besluiten op apparaat zouden voor om het even welke A/B of XT activiteiten moeten worden gebruikt die op hoogst verhandelde pagina&#39;s moeten worden geleverd, waar de prestaties zeer uw zakenKPIs zoals omzetting, opbrengst, en behoud beïnvloeden. Stel dat uw marketingteam advertentiecampagnes uitvoert om vooruitzichten voor uw homepage aan te trekken. Het runnen van advertentiecampagnes op uitgeversnetwerken vereist betaling, daarom om het even welk vooruitzicht dat op uw homepage land aan een dollarbedrag vertaalt. Stel tegelijkertijd dat u A/B-experimenten uitvoert om te zien welke hoofdafbeelding het beste de aandacht van uw consument weergeeft. Als deze A/B-experimenten nog twee seconden duren, is het zeer waarschijnlijk dat de consument ongeduldig en stuitend wordt. Daar gaan je marketingdollars en A/B-experimenten! Het verliezen van dit hard-verdiende vooruitzicht is moeilijk, aangezien om het even welke kans om dit vooruitzicht in een loyale of herhaalde klant om te zetten nu verbeurd is. Daarom kan het runnen van een op apparaat beslissingsactiviteit voor dit gebruiksgeval om het even welk negatief effect vermijden dat latentie kan introduceren.

Anderzijds, vereist het randbesluit een netwerk blokkerende vraag om een ervaring terug te winnen, maar kan zeer nuttig zijn, aangezien de gegevens in real time en ML kunnen worden gebruikt om de eindgebruikerervaring hoogst het in dienst nemen te maken. Een netwerk die vraag blokkeert zal extra latentie introduceren wanneer het leveren van de ervaring; nochtans, in sommige scenario&#39;s, kan deze compromis steek houden. Neem bijvoorbeeld een scenario waarin een klant door de productcatalogus bladert en veronderstel dat de klant naar een pagina met productdetails navigeert. Als op die pagina een aanbevolen lijst met producten wordt weergegeven, samen met het product dat de klant momenteel bekijkt, kan dit de betrokkenheid verhogen, en later de conversie en de inkomsten. Terwijl het tonen van de geadviseerde lijst van producten op deze manier een randbesluit zou vereisen dat door Adobe Target ML wordt beïnvloed algoritme-betekenend zou er toegevoegde latentie-die toegevoegde latentie niet significant genoeg voor de eindgebruiker zijn om te stuiteren. Bovendien wordt een aanbevolen lijst met producten vertaald naar een hogere omrekeningskoers. Daarom in dit geval, verstrekt een randbesluit uw zaken de meeste waarde.

## Ondersteunde functies

Naast het beoordelen van uw gebruiksgevallen en bedrijfsdoelstellingen, herzie welke eigenschappen op apparaat het beslissen [supports](../on-device-decisioning/supported-features.md) voordat u besluit of u op het apparaat moet beslissen of u randbeslissingen wilt gebruiken. Op dit moment worden bij het bepalen van randen alle typen activiteiten, doelgroepen en toewijzingsmethoden ondersteund.