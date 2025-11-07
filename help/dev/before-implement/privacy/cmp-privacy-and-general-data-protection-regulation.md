---
keywords: gdpr, eu, europese unie, privacy, faq, vaak gestelde vragen, ccpa, privacy, gegevensbescherming, opt-out, opt-out, regering, regulering, gdpr5, gdpr6, gdpr7, gdpr8, gdpr9, eu0, eu1, eu2, eu3, eu4, eu5
description: Leer over Doel en de Algemene Verordening van de Europese Unie van de Bescherming van Gegevens (GDPR), de Wet van de Consumentenprivacy van Californië (CCPA), en andere privacyvereisten.
title: Hoe handelt Target Privacy- en gegevensbeschermingsregels af?
feature: Privacy & Security
exl-id: 40bac3c5-8e6f-4a90-ac0c-eddce1dbe6c0
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '2329'
ht-degree: 0%

---

# Regels inzake privacy en gegevensbescherming

Informatie over de algemene gegevensbeschermingsverordening van de Europese Unie (GDPR), de California Consumer Privacy Act (CCPA) en andere internationale privacyvereisten. Leer hoe deze regels van invloed zijn op uw organisatie en Adobe Target.

## Overzicht van privacy en algemene gegevensbeschermingsverordening (GDPR)

Op 25 mei 2018 is de GDPR van de Europese Unie van kracht geworden. Voor meer informatie over wat deze verordening voor u betekent, zie [&#x200B; GDPR en Uw Zaken &#x200B;](https://business.adobe.com/nl/privacy/general-data-protection-regulation.html).

Wanneer Adobe software en services levert aan een onderneming, treedt Adobe op als gegevensprocessor voor persoonlijke gegevens die het verwerkt en opslaat als onderdeel van het aanbieden van deze services. Als gegevensverwerker verwerkt Adobe persoonlijke gegevens volgens de toestemming en instructies van uw bedrijf (bijvoorbeeld zoals uiteengezet in uw overeenkomst met Adobe).

Als Data Controller, bepaalt u de persoonlijke gegevens die Adobe verwerkt en namens u opslaat. Als u Adobe Experience Cloud-oplossingen gebruikt, kan Adobe persoonlijke gegevens voor u hosten, afhankelijk van de oplossingen die u gebruikt en de informatie die u kiest om naar uw Adobe Experience Cloud-account te verzenden. Voor een gedetailleerde lijst van voorbeelden, zie [&#x200B; Privacy van Adobe Experience Cloud &#x200B;](https://www.adobe.com/privacy/experience-cloud.html#collect).

Adobe Experience Cloud biedt API&#39;s die geschikt zijn voor GDPR voor gegevenscontrollers waarmee ze de volgende taken kunnen uitvoeren:

* Toegang tot informatie over betrokkenen die is opgeslagen binnen Target
* Gegevens van gegevensonderwerp die zijn opgeslagen binnen Doel verwijderen

Zie voor meer informatie:

* [&#x200B; Adobe Privacy Service overzicht &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=nl-NL)
* [&#x200B; Privacy Service API gids &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/privacy/api/overview.html?lang=nl-NL)
* [&#x200B; overzicht van Privacy Service UI &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=nl-NL)

## Overzicht van de California Consumer Privacy Act (CCPA)

De California Consumer Privacy Act (CCPA) biedt Californische consumenten nieuwe rechten met betrekking tot hun persoonlijke gegevens en legt gegevensbeschermingsverantwoordelijkheden op aan bepaalde entiteiten die zaken in Californië leiden. De CCPA is op 1 januari 2020 in werking getreden.

Op hoog niveau verleent de wet Californië verschillende belangrijke rechten, waaronder rechten op:

* Verzoek om informatie (gegevenstoegang)
* Afzien van de verkoop van persoonlijke informatie (een breed gedefinieerd recht om af te zien van het delen van informatie met derden)
* Persoonlijke gegevens verwijderen
* ervan in kennis worden gesteld dat persoonsgegevens openbaar worden gemaakt of worden verkocht

Als u zich vorig jaar bezig zou houden met het voorbereiden van de Europese privacywet (GDPR), zouden sommige van deze rechten bekend kunnen zijn en zou veel van het werk dat u hebt gedaan, kunnen worden hergebruikt.

>[!NOTE]
>
>De toegang tot en het schrappen van gegevens zoals die op CCPA van toepassing zijn volgt het zelfde proces zoals voor GDPR.

## Adobe Target- en Adobe Experience Platform-opt-in

Het doel biedt ondersteuning voor aanmeldingsfuncties via tags in Adobe Experience Platform om uw strategie voor het beheer van machtigingen te ondersteunen. Met de functie Inschakelen kunnen klanten bepalen hoe en wanneer de tag Doel wordt geactiveerd. Via Adobe Experience Platform kunt u ook de tag Doel vooraf goedkeuren. Als u de mogelijkheid wilt inschakelen om Opt-In te gebruiken in de bibliotheek Target at.js, moet u `targetGlobalSettings` gebruiken en de instelling `optinEnabled=true` toevoegen. Selecteer in Adobe Experience Platform de optie &quot;inschakelen&quot; in de vervolgkeuzelijst GDPR Inschakelen in de installatieweergave van de extensie. Zie [&#x200B; Doel uitvoeren gebruikend Adobe Experience Platform &#x200B;](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) voor meer details.

In het volgende codefragment wordt getoond hoe u de instelling `optinEnabled=true` kunt inschakelen:

```
window.targetGlobalSettings = {
  optinEnabled: true
};
```

>[!NOTE]
>
>De aanmeldingsfunctionaliteit wordt ondersteund in at.js versie 1.7.0 en at.js 2.1.0 of hoger. Inschakelen wordt niet ondersteund in at.js versie 2.0.0 en 2.0.1.

Het gebruik van Adobe Experience Platform voor het beheer van opt-in is de aanbevolen aanpak. Er is meer korrelige controle beschikbaar in Adobe Experience Platform om geselecteerde elementen van uw pagina vóór het starten van Target te verbergen. Deze elementen zijn handig als onderdeel van uw toestemmingsstrategie.

Er zijn drie scenario&#39;s om te overwegen wanneer het gebruiken van Opt-binnen:

1. **de markering van het Doel wordt vooraf goedgekeurd via Adobe Experience Platform (of het gegevenssubject eerder goedgekeurd Doel):** De markering van het Doel wordt niet gehouden voor toestemming en functies zoals verwacht.
1. **de markering van het Doel is NIET vooraf goedgekeurd en `bodyHidingEnabled` is VALS:** de markering van het Doel brandt slechts nadat de toestemming van de klant wordt verzameld. Voordat toestemming wordt verzameld, is alleen de standaardinhoud beschikbaar. Nadat de toestemming wordt ontvangen, wordt Doel geroepen en de gepersonaliseerde inhoud is beschikbaar aan de betrokkene (bezoeker). Omdat alleen de standaardinhoud beschikbaar is vóór de toestemming, is het belangrijk om een geschikte strategie te gebruiken, zoals een welkomstpagina die een gedeelte van de pagina of inhoud beslaat die kan worden gepersonaliseerd. Dit proces zorgt ervoor dat de ervaring voor de betrokkene (bezoeker) consistent blijft.
1. **de markering van het Doel is NIET vooraf goedgekeurd en `bodyHidingEnabled` is WAAR:** de markering van het Doel brandt slechts nadat de toestemming van de klant wordt verzameld. Voordat toestemming wordt verzameld, is alleen de standaardinhoud beschikbaar. Omdat `bodyHidingEnabled` is ingesteld op true, bepaalt `bodyHiddenStyle` echter welke inhoud op de pagina wordt verborgen totdat de doeltag wordt geactiveerd (of de betrokkene de aanmeldingsnaam weigert, in welk geval de standaardinhoud wordt weergegeven). Standaard is `bodyHiddenStyle` ingesteld op `body { opacity:0;}` , waardoor de body-tag van HTML wordt verborgen. De door Adobe aanbevolen paginaconfiguratie is hieronder weergegeven, zodat de volledige hoofdtekst van de pagina, behalve het dialoogvenster voor het beheer van de toestemming, wordt verborgen door de inhoud van de pagina in één container te plaatsen en het dialoogvenster voor het beheer van de toestemming in een aparte container. Met deze instelling configureert u Doel zodanig dat alleen de container van de pagina-inhoud wordt verborgen. Zie het [&#x200B; overzicht van Privacy Service &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=nl-NL&).

   De geadviseerde pagina opstelling voor scenario 3 is:

   ```
   <html> 
   <head> 
   //visitor, at.js 
   </head> 
   
   <body> 
   <div id = "consentManagerDialog"> 
   
   //consent manager html dialog goes here 
   </div> 
   
   <div id="pageContent"> 
   // page content goes here 
   </div> 
   
   </body> 
   </html> 
   ```

   Ervan uitgaande dat `bodyHiddenStyle` van:

   ```
   #pageContent { opacity:0;}
   ```

## Privacy- en gegevensbeschermingsregels Veelgestelde vragen

Veelgestelde vragen over de algemene gegevensbeschermingsverordening (GDPR) van de Europese Unie, de California Consumer Privacy Act (CCPA) en andere specifieke internationale privacyvereisten voor Target.

### Wat is het beleid van Adobe voor deze regelgeving?

Adobe voldoet al aan of voert zijn verplichtingen als gegevensverwerker uit. Adobe heeft een sterke basis voor gecertificeerde beveiliging en privacycontroles door ontwerp en heeft productverbeteringen doorgevoerd vóór de deadline van mei 2018. De klanten van de onderneming hebben de verantwoordelijkheid om deze verhogingen uit te voeren en om het even welk noodzakelijk beleid en procedures bij te werken.

### Moet mijn bedrijf, het Controlemechanisme van Gegevens, een GDPR of CCPA- verzoek aan elke oplossing van Adobe Experience Cloud voorleggen die het gebruikt?

Nee, Adobe biedt een centrale manier om gegevenscontrollers te helpen voldoen aan hun GDPR- en CCPA-vereisten. Gegevenscontrollers hoeven niet rechtstreeks naar elke oplossing te gaan.

Alle GDPR- en CCPA-aanvragen in Experience Cloud-oplossingen, waaronder Target, worden uitgevoerd via een centrale Adobe API, die momenteel de GDPR API wordt genoemd. De API voltooit de aanvraag vervolgens via de Experience Cloud-oplossing van de Data Controller.

### Met welke informatie kunnen klanten door Adobe worden verwijderd als reactie op een verzoek van een betrokkene of gebruiker?

De informatie met betrekking tot een individuele bezoeker binnen Doel is opgenomen in het profiel van de Doelbezoeker. Met Doel kunnen klanten alle gegevens verwijderen die aan een id zijn gekoppeld in hun bezoekersprofiel. Voor voorbeelden van de opslag van het profielgegevensdoel, zie [&#x200B; Profiel van de Bezoeker &#x200B;](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=nl-NL).

Geaggregeerde of geanonimiseerde gegevens (bijvoorbeeld gegevens die een bepaalde persoon niet identificeren) of gegevens die geen verband houden met een specifieke persoon (bijvoorbeeld inhoudsgegevens), vallen buiten het bereik van een verzoek tot verwijdering van een gebruiker.

Profielen voor doelbezoekers die 90 dagen inactief zijn, worden standaard verwijderd, zonder dat een actie vereist is.

### Welke IDs wordt gesteund om klanten te helpen een GDPR of CCPA toegang en schrappingsverzoek voor Doel voltooien?

Het doel ondersteunt de volgende id-typen om een klantprofiel te zoeken:

| Gebruikersnaam | Naam ruimte-id-type | Naamruimte-id | Definitie |
|--- |--- |--- |--- |
| Experience Cloud-id (ECID) | Standaard | 4 | Adobe Experience Cloud ID, voorheen bekend als bezoeker-ID of Experience Cloud-ID. U kunt de JavaScript API gebruiken om deze id te zoeken (zie hieronder voor meer informatie). |
| TnT-id / Cookie-id (TNTID) | Standaard | 9 | Doel-id ingesteld als een cookie in de browser van de bezoeker. U kunt de JavaScript API gebruiken om deze id te zoeken (zie hieronder voor meer informatie). |
| ID/CRM-ID van derden (DERDE PARTYID) | Doelspecifiek | NVT | Als u Target van uw CRM of andere unieke herkenningstekeninformatie voor uw klanten voorziet. |

>[!NOTE]
>
>Hoewel Target zowel cookies van derden als cookies van andere leveranciers ondersteunt, worden cookies van het type First-party Target alleen aangeraden voor GDPR en CCPA.

### Hoe behandelt Target toestemmingsbeheer?

GDPR en CCPA veranderen niet wanneer u toestemming moet krijgen, maar hoe u het krijgt. De toestemmingsstrategie van elke klant hangt van zijn gegevensinzameling en gebruikspraktijken en zijn privacybeleid af. Het beheer van de toestemming wordt niet gesteund door en zou niet via Doel voor GDPR en CCPA moeten worden bereikt.

Adobe biedt momenteel geen oplossing voor het beheer van instemming, maar er zijn verschillende instrumenten die zich op de markt ontwikkelen om aan een aantal van de nieuwe vereisten te voldoen. Voor meer informatie over privacyhulpmiddelen in het algemeen, met inbegrip van toestemmingsmanagers, zie het [&#x200B; 2017 Rapport van de Technische Verkoper van de Privacy &#x200B;](https://iapp.org/media/pdf/resource_center/Tech-Vendor-Directory-1.4.1-electronic.pdf) op de *Internationale Vereniging van de Beroeps van de Privacy (iaap)* website.

Het doel biedt ondersteuning voor aanmeldingsfuncties via Adobe Experience Platform ter ondersteuning van uw strategie voor het beheer van machtigingen. Met de functie Inschakelen kunnen klanten bepalen hoe en wanneer de tag Doel wordt geactiveerd. Via Adobe Experience Platform kunt u ook de tag Doel vooraf goedkeuren. Het gebruik van Adobe Experience Platform voor het beheer van opt-in is de aanbevolen aanpak. Er is meer korrelige controle beschikbaar in Adobe Experience Platform om bepaalde elementen van uw pagina te verbergen vóór het afvuren van het Doel. Dit kan handig zijn als onderdeel van uw toestemmingsstrategie.

Voor meer informatie over GDPR, CCPA, en Adobe Experience Platform, zie [&#x200B; de Bibliotheek van JavaScript van de Privacy van Adobe en GDPR &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=nl-NL&). Ook, zie *Adobe Target en Adobe Experience Platform hierboven opt-in* sectie.

### Verzendt `AdobePrivacy.js` informatie naar de GDPR API?

AdobePrivacy.js legt ** deze informatie aan API niet voor. De klant moet dat doen. Deze bibliotheek bevat alleen de id&#39;s die in de browser voor die specifieke bezoeker zijn opgeslagen.

### Wat verwijdert `removeIdentities`?

`removeIdentities` *slechts* verwijdert die identiteiten uit browser, en dat slechts afhangt van of de oplossing van Adobe het heeft uitgevoerd.

Doel verwijdert bijvoorbeeld de cookies waarin de id&#39;s worden opgeslagen, maar Adobe Audience Manager (AAM) verwijdert de index-id die is opgeslagen in een cookie van een andere fabrikant niet.

### Welke informatie moet in een GDPR- of CCPA-aanvraag van Target worden opgenomen?

Naast de vereisten van Centraal Privacy Service bevat een geldig GDPR- of CCPA-bericht voor Target:

```
{ 
    "jobId":"12345AD43E", 
    ... 
    "products":["Target",...], 
    "companyContexts":[ 
        { 
            "namespace":"imsOrgID", 
            "value":"123456789@AdobeOrg" 
        }, 
        ... 
    ], 
    "userContexts":[ 
        { 
            "namespace":"ECID", 
            "namespaceId":4, 
            "type":"standard", 
            "value":"53792210477379708453829363835595041181" 
        } 
        And/OR: 
        { 
            "namespace":"TNTID", 
            "namespaceId":9, 
            "type":"standard", 
            "value":"1234567890" 
        } 
        And/OR: 
        { 
            "namespace":"THIRDPARTYID", 
            "type":"target", 
            "value":"thirdPartyIdName" 
        }, 
        ... 
    ] 
}
```

### Welke soorten reacties kan ik verwachten van Target via de GDPR API?

| Aanvraagstatus | Doelresponsbericht | Scenario |
|--- |--- |--- |
| Verwerking | Verwerking | Doel heeft het verzoek van GDPR of CCPA ontvangen en verwerkt dit. |
| Voltooid | Niet van toepassing - bedrijfcontext niet van toepassing | De IMS-id in het GDPR- of CCPA-verzoek wordt niet toegewezen aan een doelclient.<br /> Sommige bedrijven hebben veelvoudige IMS IDs. Verzend de IMS-id waarin Target is ingericht. |
| Voltooid | Niet van toepassing - gebruikerscontext niet gevonden | De in het verzoek van de GDPR of de CCPA voor de specifieke bezoeker of betrokkene verstrekte id is niet aanwezig in de Target profile store.<br /> Dit resultaat keert ook terug als u probeert om een type van namespaceidentiteitskaart voor te leggen dat niet door Doel (zie hierboven voor gesteunde IDs) wordt gesteund. |
| Fout | Foutbericht (details zijn afhankelijk van het type fout) | Fout bij het ophalen of verwijderen van het gewenste gegevensonderwerpprofiel.<br /> Fout terwijl het uploaden aan Azure voor toegangsverzoek. |

### Welke reactie verzendt Target naar de GDPR API voor een toegangsverzoek?

Reacties op verzoeken om toegang tot gegevens bevatten een samenvatting van het doelprofiel voor de betrokken bezoeker. Deze terugkeer wordt verzonden naar de Experience Cloud GDPR API, die op zijn beurt de Controllers van Gegevens een reactie verzendt.

Een voorbeeld van de API-respons voor doeltoegang kan er als volgt uitzien:

```
{ 
    "jobId":"12345AD43E", 
    ... 
    "products":["Target",...], 
    "companyContexts":[ 
        { 
            "namespace":"imsOrgID", 
            "value":"123456789@AdobeOrg" 
        }, 
        ... 
    ], 
    "userContexts":[ 
        { 
            ~"namespace":"ECID", 
            "namespaceId":4, 
            "type":"standard", 
            "value":"53792210477379708453829363835595041181" 
        } 
        And/OR: 
        { 
            ~"namespace":"tntId", 
            "namespaceId":9, 
            "type":"standard", 
            "value":"1234567890" 
        } 
        And/OR: 
        { 
            "namespace":"thirdPartyId", 
            "type":"target", 
            "value":"thirdPartyIdName" 
        }, 
        ... 
    ] 
} 
```

| Veld | Beschrijving |
|--- |--- |
| jobId | Hiermee wordt de GDPR- of CCPA-taak-id van de centrale GDPR-API aangegeven. |
| imsOrgID | Verstrekt een uniek herkenningsteken voor uw bedrijf. |
| namespace | Wordt ook wel gegevensbron genoemd. Zie &quot;Welke IDs wordt gesteund om klanten te helpen een GDPR of CCPA toegang en schrappingsverzoek voor Doel voltooien?&quot; in dit onderwerp. |
| type | Het type van identiteitskaart waarvoor u GDPR of CCPA gegevenstoegang vroeg. Het doel keurt verscheidene types van identiteitskaart goed, waarvan sommige standaard en sommige specifiek voor Doel zijn. Zie &quot;Welke IDs wordt gesteund om klanten te helpen een GDPR of CCPA toegang en schrappingsverzoek voor Doel voltooien?&quot; in dit onderwerp. |
| value | De id van de naamruimte/gegevensbron. Zie &quot;Welke IDs wordt gesteund om klanten te helpen een GDPR of CCPA toegang en schrappingsverzoek voor Doel voltooien?&quot; voor geaccepteerde waarden. |
| integratiecode | De codes van de integratie zijn vriendschappelijke namen voor uw gegevensbronnen en helpen u uw gegevensbronnen volgen gemakkelijker dan het gebruiken van gegevensbron IDs. |

Als er meerdere waarden zijn opgegeven om profielen te identificeren, heeft elke geldige id één profielbestand. Een of meer profielbestanden worden via de GDPR Central API naar de centrale GDPR Azure Blob verzonden, in de vorm van de JSON-respons voor Target Profile.

Een voorbeeld van een doelprofiel voor JSON kan er als volgt uitzien:

```
{"profileAttributes": 
 
"Sample_Parameter":{"value":"Gold Loyalty Status","modifiedAt":"2018-04-11T21:44:14.000-04:00"}, 
 
"user.ReturnTimeOfDay":{"value":"44.0","modifiedAt":"2018-04-11T21:44:14.000-04:00"}, 
 
"firstSessionStart":{"value":"1523497450602","modifiedAt":"2018-04-11T21:44:10.000-04:00"}, 
 
"user.sessionCountScript":{"value":"1","modifiedAt":"2018-04-11T21:44:14.000-04:00"} 
   } 
} 
```

De volgende tabel bevat een beschrijving van de JSON-velden voor het illustratieve profiel:

| Veld | Beschrijving |
|--- |--- |
| sample_parameter | Veel gegevens in het doelprofiel worden geüpload of rechtstreeks geleverd door de gegevenscontroller. In dit voorbeeld is een parameter geüpload naar het doelprofiel met de API voor profielupdate. Voor meer informatie, zie [&#x200B; Methoden om Gegevens in Doel &#x200B;](/help/dev/before-implement/methods-to-get-data-into-target/methods-to-get-data-into-target.md) te krijgen. |
| user.ReturnTimeOfDay | Dit standaardveld bevat de tijd van de dag van het meest recente retourbezoek van een gebruiker. |
| firstSessionStart | Dit standaardveld bevat de tijd van de dag waarop de eerste sessie van de gebruiker is gestart. |
| user.sessionCountScript | Veel gegevens in het doelprofiel worden geüpload of rechtstreeks geleverd door de gegevenscontroller. In dit voorbeeld verhoogt een profielscript het aantal sessies dat deze bezoeker op de site van de Data Controller heeft uitgevoerd. Voor meer informatie, zie {de Attributen van het Manuscript van 0} Profiel [.](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=nl-NL) |

>[!NOTE]
>
>Dit codevoorbeeld is een verkorte versie van een JSON-doelprofiel ter illustratie. Veel velden van het doelprofiel zijn niet standaard. Wat wordt geretourneerd, is afhankelijk van de informatie in dat specifieke bezoekersprofiel.

### Steunt het Doel IP verduistering?

Het doel steunt IP verwarring als u verkiest om het als deel van uw GDPR of CCPA implementatiestrategie te gebruiken. Voor meer informatie, zie [&#x200B; Privacy &#x200B;](privacy.md#replacement-of-last-octet-of-ip-addresses).

### Moet ik iets doen om te voorkomen dat mijn gegevens worden gedeeld of verkocht aan derden?

Met Target kunnen klanten geen gegevens rechtstreeks van Target aan derden delen of verkopen, zodat er geen sprake is van een opt-out voor Target.
