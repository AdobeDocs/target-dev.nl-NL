---
keywords: at.js, browser gebruikersagent, gebruikersagent, cliëntwenken, gebruiker-agent
description: Leer hoe Adobe Target de gebruikersagent en de Tips van de Cliënt gebruikt om bezoekers voor segmentatie en verpersoonlijking te kwalificeren.
title: Gebruikersagent en clienttips
feature: at.js
exl-id: e0d87d95-ee95-4ca9-8632-222ae1fb9a91
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 0%

---

# Gebruiker-agent en de wenken van de Cliënt

Adobe Target gebruikt de user-agent om bezoekers voor segmentatie en verpersoonlijking te kwalificeren.

>[!NOTE]
>
>De informatie in dit artikel is op [ at.js versie 2.9.0 ](target-atjs-versions.md) (of later) van toepassing.

Telkens wanneer een webbrowser een verzoek indient bij een server, wordt informatie over de browser en de omgeving waarin de browser wordt uitgevoerd, opgenomen in de koptekst van de aanvraag. Sinds de vroege dagen van Internet, zijn deze gegevens bijeengevoegd in één enkel koord genoemd user-agent.

De volgende tekst is een voorbeeld van een gebruiker-agent van een op Mac OS X-Gebaseerde computer die een Browser Safari gebruikt:

```
Mozilla/5.0 (Linux; Android 12; SM-S908E) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.41 Mobile Safari/537.36 
```

Van deze user-agent, kan de server die het verzoek ontvangt de volgende informatie over browser en werkend systeem ontdekken:

| Informatie | Details |
| --- | --- |
| Naam software | Chrome |
| Softwareversie | 101 |
| Volledige softwareversie | 101.0.4951.41 |
| Naam van lay-outengine | AppleWebKit |
| Versie van lay-outengine | 537,36 |
| Besturingssysteem | Android |
| Versie besturingssysteem | Android 12 (sneeuwkegel) |
| Apparaat | SM-S908E (Samsung Galaxy S22 Ultra) |

In de loop der jaren is de hoeveelheid browser- en apparaatinformatie in de user-agent-tekenreeks toegenomen.

## Gebruiksgevallen van gebruikersagenten

De gebruiker-agenten zijn lang gebruikt om marketing en ontwikkelaarteams van belangrijke inzichten in te voorzien hoe browsers, werkende systemen, en apparaten plaatsinhoud tonen, evenals hoe de gebruikers met websites in wisselwerking staan. De gebruiker-agenten worden ook gebruikt om spam en filterbots te blokkeren die plaatsen voor een verscheidenheid van extra doeleinden kruipen.

In de afgelopen jaren hebben sommige eigenaars van sites en marketingverkopers de gebruikersagent echter samen met andere informatie in aanvraagheaders gebruikt om digitale vingerafdrukken te maken die kunnen worden gebruikt om gebruikers zonder hun medeweten te identificeren. Ondanks het belangrijke doel dat de gebruiker-agent voor plaatseigenaren dient, hebben de browser ontwikkelaars besloten om veranderingen in te brengen hoe user-agents werken om potentiële privacykwesties voor plaatsbezoekers te beperken.

Browser ontwikkelaars creeerden Gebruiker-Agent de Tips van de Cliënt als oplossing aan deze uitdaging. Met behulp van de tinten van de client kunnen sites nog steeds de benodigde browser, het besturingssysteem en apparaatinformatie verzamelen, terwijl ze tegelijkertijd een betere bescherming bieden tegen methoden voor het bijhouden van gegevens, zoals vingerafdrukken.

## Clienttips

De gebruikers-Agent wenken van de Cliënt verstrekken websiteeigenaars de capaciteit om tot veel van de zelfde informatie toegang te hebben beschikbaar in gebruiker-agent, maar op een meer privacy-bewarende manier. Wanneer moderne browsers een user-agent naar een Webserver verzenden, wordt de volledige user-agent verzonden op elk verzoek, ongeacht of het wordt vereist. Clienttips daarentegen dwingen een model in waarin de server de browser om aanvullende informatie over de client moet vragen. Op het ontvangen van dit verzoek, kan browser zijn eigen beleid of gebruiker-configuratie toepassen om te bepalen welke gegevens zijn teruggekeerd. In plaats van de volledige gebruiker-agent door gebrek op alle verzoeken bloot te stellen, wordt de toegang nu geleid op een expliciete en controleerbare manier.

Client Hints voor gebruikersagent zijn sinds versie 89 beschikbaar in Chrome. Recente versies van Chromium-gebaseerde browsers, zoals Microsoft Edge, Opera, Brave, Chrome Android, Opera Android en Samsung Internet, ondersteunen ook de client Hints-API.

De wenken van de cliënt in de kopballen van het eerste verzoek dat door browser aan een Webserver wordt gemaakt bevatten het browser merk, de belangrijkste versie van browser, en een indicator van of de cliënt een mobiel apparaat is. Elk stuk gegevens heeft zijn eigen kopbalwaarde, eerder dan wordt gegroepeerd in één gebruiker-agent koord.

Hier volgen bijvoorbeeld enkele tips voor clients:

```
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99" 
Sec-CH-UA-Mobile: ?0 
Sec-CH-UA-Platform: "macOS"
```

...while this is the user-agent for the same browser:

```
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36 
```

Hoewel de informatie gelijkaardig is, bevat het eerste verzoek aan de server de Tips van de Cliënt die slechts een ondergroep van wat in het user-agent koord beschikbaar is bevat. De aanvraag heeft geen betrekking op de architectuur van het besturingssysteem, de volledige versie van het besturingssysteem, de naam van de opmaakengine, de versie van de opmaakengine en de volledige browserversie. Bij volgende aanvragen staat de client Hints-API webservers echter wel toe om aanvullende, hoge entropiedetails over het apparaat te vragen. Wanneer deze hoge entropiewaarden worden gevraagd, afhankelijk van het browserbeleid of gebruikersinstellingen, kan de browserreactie die informatie bevatten.

In het volgende voorbeeld ziet u een JSON-object dat door de client Hints-API wordt geretourneerd wanneer hoge entropiewaarden worden aangevraagd:

```
{ 

    "architecture":"x86", 
    "bitness":"64", 
    "brands":[ 
        { 
            "brand":" Not A;Brand", 
            "version":"99" 
        }, 
        { 
            "brand":"Chromium", 
            "version":"100" 
        }, 
        { 
            "brand":"Google Chrome", 
            "version":"100" 
        } 
    ], 
    "fullVersionList":[ 
        { 
            "brand":" Not A;Brand", 
            "version":"99.0.0.0" 
        }, 
        { 
            "brand":"Chromium", 
            "version":"100.0.4896.127" 
        }, 
        { 
            "brand":"Google Chrome", 
            "version":"100.0.4896.127" 
        } 
    ], 
    "mobile":false, 
    "model":"", 
    "platformVersion":"12.2.1" 
} 
```

De hoge entropiewaarden omvatten verscheidene extra stukken van informatie die niet in de standaardinformatie van de wenken van de Cliënt beschikbaar zijn. De volgende lijst bevat details van welke gegevens in het standaardverzoek tegenover de hoge entropie gebruiker-Agent informatie van de Cliënt beschikbaar zijn.

| HTTP-header | JavaScript | Gebruikersagent | Clienttip | Hoog entropclientijd |
| --- | --- | --- | --- | --- |
| Sec-CH-UA | merken | Ja | Ja | Nee |
| Sec-CH-UA-Platform | platform | Ja | Ja | Nee |
| Sec-CH-UA-Mobile | mobiel | Ja | Ja | Nee |
| Sec-CH-UA-Platform-Version | platformVersion | Ja | Nee | Ja |
| Sec-CH-UA-Arch | architectuur | Ja | Nee | Ja |
| Sec-CH-UA-model | model | Ja | Nee | Ja |
| Sec-CH-UA-Bitness | Bitsheid | Ja | Nee | Ja |
| Sec-CH-UA-Full-Version-List | fullVersionList | Ja | Nee | Ja |

## Migratie naar clienttips

Op dit moment blijven op chroom gebaseerde browsers de user-agent samen met de Tips van de Cliënt in de kopballen van verzoeken verzenden die aan Webservers worden gemaakt. Vanaf april 2022 en tot februari 2023 wordt de hoeveelheid gegevens in de user-agent-tekenreeks echter verminderd. Andere browsers, zoals Safari en Firefox, blijven gebruikmaken van de user-agent-tekenreeks, maar ook zij zullen de hoeveelheid informatie in die reeks verminderen.

## Gebruiksscenario&#39;s voor doelgebruik waarvoor clienttips vereist zijn

De volgende gebruiksgevallen in Doel vereisen de wenken van de Cliënt:

### Kenmerken publiek

Als u het publiek van het Doel gebruikt en om het even welke volgende publieksattributen gebruikt, vereist het Doel de wenken van de Cliënt om de correcte segmentatie uit te voeren:

* Browser
* Besturingssysteem
* Mobiel

### Profielscripts

Als u profielscripts gebruikt en naar het kenmerk `user.browser` verwijst (dat naar user-agent verwijst), moet u mogelijk het profielscript bijwerken om een of meer clienttips te controleren. U hebt toegang tot alle clienttips met de functie `user.clientHint('sec-ch-ua-xxxxx')` . De naam van de header van de client-tip moet allemaal in kleine letters zijn.

In het volgende voorbeeld ziet u hoe u een Windows-besturingssysteem correct detecteert in een profielscript:

```
"return (((user.browser != null) && (user.browser.indexOf(\"Windows\") > -1)) || " + 
      "((user.clientHint('sec-ch-ua-platform') != null) && 
(user.clientHint('sec-ch-ua-platform') === 'Windows')));" 
```

Hier is een lijst van de wenken van de Cliënt en hun overeenkomstige het gebruiksemantiek van het profielmanuscript.

| Clienttip | Entropie | Auditiekenmerk | Gebruik van profielscript |
| --- | --- | --- | --- |
| [ sec-CH-UA ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA) | Laag | Browser | `user.clientHint('sec-ch-ua')` |
| [ Sec-CH-UA-Arch ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Arch) | Hoog | Aan gebruikers beschikbaar via profielscripts | `user.clientHint('sec-ch-ua-arch')` |
| [ sec-CH-UA-Bitness ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Bitness) | Hoog | Aan gebruikers beschikbaar via profielscripts | `user.clientHint('sec-ch-ua-bitness')` |
| [ sec-CH-UA-Volledig-Versie-Lijst ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Full-Version-List) | Hoog | Browser | `user.clientHint('sec-ch-ua-full-version-list')` |
| [ sec-CH-UA-Mobiel ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Mobile) | Laag | Mobiel | `user.clientHint('sec-ch-ua-mobile')` |
| [ sec-CH-UA-Model ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Model) | Hoog | Mobiel | `user.clientHint('sec-ch-ua-model')` |
| [ sec-CH-UA-Platform ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Platform) | Laag | Besturingssysteem | `user.clientHint('sec-ch-ua-platform')` |
| [ sec-CH-UA-Platform-Versie ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Platform-Version) | Hoog | Aan gebruikers beschikbaar via profielscripts | `user.clientHint('sec-ch-ua-platform-version')` |

## Clienttips doorgeven aan Adobe Target

De volgende secties bevatten meer informatie over hoe te om de wenken van de Cliënt, afhankelijk van uw implementatie van het Doel over te gaan.

### at.js versie 2.9.0 (of hoger)

Vanaf at.js 2.9.0 worden de Tips van de Cliënt van de Agent van de Gebruiker automatisch verzameld van browser en verzonden naar Doel wanneer `getOffer/getOffers()` wordt geroepen. Standaard verzamelt at at.js alleen &#39;Low Entropy&#39;-clienttips. Als het uitvoeren van publiekssegmentatie of het gebruiken van profielmanuscripten die op gegevens worden gebaseerd die als &quot;Hoge Entropie&quot;van de voorafgaande secties worden gecategoriseerd, moet u at.js vormen om &quot;Hoge Tips van de Cliënt Entropie&quot;van browser via `targetGlobalSettings` te verzamelen.

```
window.targetGlobalSettings = { allowHighEntropyClientHints: true };
```

### SDK&#39;s aan serverzijde

Voor meer informatie over hoe te om de wenken van de Cliënt via server-kant SDKs over te gaan, zie [ wenken van de Cliënt ](../../server-side/sdk-guides/core-principles/audience-targeting.md#client-hints) onder Server-kant de documentatie van de Implementatie.
