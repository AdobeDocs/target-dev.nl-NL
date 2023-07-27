---
keywords: privacy, ip-adres, geosegmentatie, opt-out, optout, opt-out, gegevensprivacy, overheidsverordeningen, verordeningen, gdpr, ccpa, privacy, persoonlijk identificeerbare informatie, PII
description: Meer informatie [!DNL Adobe Target] voldoet aan de toepasselijke wetgeving op het gebied van gegevensprivacy, waaronder het verzamelen en verwerken van IP-adressen, PII's en instructies om te weigeren.
title: Hoe behandelt Target privacykwesties, inclusief PII?
feature: Privacy & Security
exl-id: 4330e034-2483-4a25-9c87-48dbef6fc9de
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# Privacy

[!DNL Adobe Target] heeft processen en instellingen ingeschakeld waarmee u kunt werken [!DNL Target] in overeenstemming met de toepasselijke wetgeving inzake gegevensbescherming.

## Verzameling van IP-adressen en persoonlijk identificeerbare informatie (PII)

Het IP-adres van een bezoeker van uw website wordt naar een Adobe Data Processing Center (DPC) verzonden. Afhankelijk van de netwerkconfiguratie voor de bezoeker, vertegenwoordigt het IP adres niet noodzakelijk het IP adres van de computer van de bezoeker. Bijvoorbeeld, zou het IP adres het externe IP adres van een firewall van het Vertaal adres van het Netwerk (NATIONAAL), de volmacht van HTTP, of de gateway van Internet kunnen zijn.

>[!IMPORTANT]
>
>[!DNL Target] slaat geen IP adressen van de gebruiker of om het even welke Persoonlijk Identificeerbare Informatie (PII) op. IP de adressen worden gebruikt slechts door [!DNL Target] tijdens de sessie (in het geheugen, nooit voortgezet).

## Vervanging van laatste octet van IP adressen

Adobe heeft een &quot;privacy-by-design&quot;-instelling ontwikkeld die gebruikers kunnen inschakelen voor Adobe [!DNL Target]. Indien ingeschakeld, Adobe [!DNL Target] onmiddellijk verduistert het laatste octet (het laatste gedeelte) van het IP adres op het tijdstip dat het IP adres wordt verzameld. Deze anonymization wordt uitgevoerd vóór om het even welke verwerking van het IP adres, met inbegrip van vóór een facultatieve geo-raadpleging van het IP adres.

Wanneer deze eigenschap wordt toegelaten, wordt het IP adres gemaakt voldoende anoniem zodat is het niet meer identificeerbaar als persoonlijke informatie. Dientengevolge, [!DNL Target] kunnen worden gebruikt in overeenstemming met de wetgeving inzake privacy van gegevens in landen die het verzamelen van persoonsgegevens niet toestaan. Het verkrijgen van informatie op het niveau van de stad zal waarschijnlijk aanzienlijk worden beïnvloed door de verduistering van het IP-adres. Het verkrijgen van informatie op regionaal en nationaal niveau mag slechts enigszins worden beïnvloed.

De volgende instellingen zijn beschikbaar in de [!DNL Target] UI door te navigeren naar **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**:

* [!UICONTROL Last octet obfuscation]: [!DNL Target] verbergt het laatste octet van het IP adres.
* [!UICONTROL Entire IP obfuscation]: [!DNL Target] verbergt het volledige IP adres.
* [!UICONTROL None]: [!DNL Target] verbergt geen enkel deel van het IP adres.

  ![obfuscate-ip-options](assets/obfuscate-ip.png)

[!DNL Target] ontvangt het volledige IP adres en verduistert het (als reeks aan Laatste octet of Volledige IP) zoals gespecificeerd. [!DNL Target] houdt dan het verduisterde IP adres in geheugen slechts tijdens de huidige zitting.

## GeoSegmentation

Als u de vervanging van het laatste octet van het IP adres toelaat, kunnen de resterende waarden van het IP adres worden geanalyseerd gebruikend rapporten in [!DNL Target]. Als het laatste octet van het IP adres niet verduisterd is geweest, dan kan het volledige IP adres binnen worden geanalyseerd [!DNL Target]. Met de functie GeoSegmentation kunt u de locatie van de bezoeker per geografisch gebied in kaart brengen. GeoSegmentation-gegevens zijn alleen granulair voor het niveau van de stad of postcode, en niet voor het individuele niveau.

Als IP de adressen volledig verduisterd zijn, is GeoSegmentation en geo het richten niet beschikbaar.

## Koppeling uitschakelen

U kunt een koppeling om te weigeren toevoegen aan uw sites zodat bezoekers zich kunnen afmelden voor alle aftellingen en de levering van inhoud.

1. Voeg de volgende koppeling toe aan uw site:

   `<a href="https://clientcode.tt.omtrdc.net/optout"> Your Opt Out Language Here</a>`

1. (Voorwaardelijk) als u CNAME gebruikt, zou de verbinding &quot;client= moeten bevatten`clientcode` parameter, bijvoorbeeld:
   `https://my.cname.domain/optout?client=clientcode`.

1. Vervangen `clientcode` met uw clientcode en voeg de tekst of afbeelding toe die u wilt koppelen aan de URL voor niet-deelname.

Elke bezoeker die op deze koppeling klikt, wordt niet opgenomen in een box-aanvraag die vanaf zijn browsersessies wordt aangeroepen totdat hij of zij zijn of haar cookies verwijdert, of gedurende twee jaar, afhankelijk van welke eerst aankomt. Dit werkt door een cookie in te stellen voor de aangeroepen bezoeker `disableClient` in de `clientcode.tt.omtrdc.net` domein.

Zelfs als u een eersteklas cookie-implementatie gebruikt, wordt de opgegeven opt-out ingesteld via een cookie van een andere fabrikant. Als de client alleen een cookie van de eerste fabrikant gebruikt, [!DNL Target] Hiermee wordt gecontroleerd of een uitschakelcookie is ingesteld.

## Regels inzake privacy en gegevensbescherming

Zie [Regels inzake privacy en gegevensbescherming](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) voor meer informatie over de algemene gegevensbeschermingsverordening van de Europese Unie (GDPR), de California Consumer Privacy Act (CCPA) en andere internationale privacyvereisten, en over de invloed die deze regels hebben op uw organisatie en [!DNL Target].

## Verzameling van gebruiksgegevens

De individuele eigenschap-gebruik gegevens worden verzameld voor interne Adobe doeleinden om te bepalen of [!DNL Target] functies worden uitgevoerd zoals bedoeld of om te bepalen welke functies onderbenut worden. Er worden verschillende metingen van de latentie verzameld om prestatieproblemen te verhelpen. Persoonlijke gegevens worden niet verzameld.

U kunt het rapporteren van gebruiksgegevens in onze SDK&#39;s uitschakelen door het instellen van `telemetryEnabled` naar false in de initialisatieopties voor de client. Zie voor meer informatie [telemetryEnabled in targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#telemetryenabled).
