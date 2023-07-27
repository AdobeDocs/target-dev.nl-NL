---
title: Overzicht van Adobe Modellen API
description: Overzicht van de Modellen API, die gebruikers kunnen gebruiken om te voorkomen dat functies worden opgenomen in modellen voor machinaal leren.
exl-id: e34b9b03-670b-4f7c-a94e-0c3cb711d8e4
feature: APIs/SDKs, Recommendations, Administration & Configuration
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 0%

---

# Modellen API - Overzicht

Met de API Modellen, ook wel de Lijst van gewezen personen-API genoemd, kunnen gebruikers de lijst met functies weergeven en beheren die in modellen voor machinaal leren worden gebruikt voor [!UICONTROL Automated Personalization] (AP) en [!DNL Auto-Target] (AT) activiteiten. Als een gebruiker een eigenschap van door de modellen voor AP of bij activiteiten zou willen uitsluiten worden gebruikt, kunnen zij Modellen API gebruiken om die eigenschap aan de &quot;lijst van gewezen personen toe te voegen.&quot;

A **[!UICONTROL blocklist]** definieert de reeks functies die worden uitgesloten door [!DNL Adobe Target] van zijn modellen voor machinaal leren. Zie voor meer informatie over functies [Door [!DNL Target] computerleeralgoritmen](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/ap-data.html).

Lijsten van gewezen personen kunnen per activiteit (activiteitsniveau) of voor alle activiteiten binnen een [!DNL Target] account (algemeen niveau).

<!-- To get started with the Models API in order to create and manage your blocklist, download the Postman Collection [here](https://git.corp.adobe.com/target/ml-configuration-management-service/tree/nextRelease/rest_api_library). Note this is an Adobe internal link. Need to publish this publicly if want to share with customers. -->

## Modellen API-specificatie

De Modellen API-specificatie weergeven [hier](../administer/models-api/models-api-overview.md).

## Vereisten

Als u de Modellen-API wilt gebruiken, moet u verificatie configureren met de [Adobe Developer Console](https://developer.adobe.com/console/home), net als bij de [API voor doelbeheer](../administer/admin-api/admin-api-overview-new.md). Zie voor meer informatie [Verificatie configureren](../before-administer/configure-authentication.md).

## Richtlijnen voor gebruik van modellen-API

Hoe te om lijsten van gewezen personen te beheren

[**Stap 1:**](#step1) Lijst met functies voor een activiteit weergeven

[**Stap 2:**](#step2) Controleer de lijst van gewezen personen van de activiteit

[**Stap 3:**](#step3) Functies toevoegen aan de lijst van gewezen personen van de activiteit

[**Stap 4:**](#step4) (Optioneel) Blokkeren opheffen

[**Stap 5:**](#step5) (Optioneel) De algemene lijst van gewezen personen beheren


## Stap 1: Lijst met functies voor een activiteit weergeven {#step1}

Voordat u een functie voegt op lijst van gewenste personen, bekijkt u de lijst met functies die momenteel worden opgenomen in de modellen voor die activiteit.

>[!BEGINTABS]

>[!TAB Verzoek]

```json {line-numbers="true"}
GET https://mc.adobe.io/<tenant>/target/models/features/<campaignId>
```

>[!TAB Antwoord]

```json {line-numbers="true"}
{
    "features": [
        {
            "externalName": "Visitor Profile - Total Visits to Activity",
            "internalName": "SES_PREVIOUS_VISIT_COUNT",
            "type": "CONTINUOUS"
        },
        {
            "externalName": "Visitor Profile - Total Visits",
            "internalName": "SES_TOTAL_SESSIONS",
            "type": "CONTINUOUS"
        },
        {
            "externalName": "Visitor Profile - Pages Seen Before Activity",
            "internalName": "SES_PREVIOUS_VISIT_COUNT",
            "type": "CONTINUOUS"
        },
        {
            "externalName": "Visitor Profile - Activity Lifetime Time on Site",
            "internalName": "SES_TOTAL_TIME",
            "type": "CONTINUOUS"
        }
    ],
    "reportParameters": {
        "clientCode": <tenant>,
        "campaignId": <campaignId>
    }
}
```

>[!ENDTABS]

<!-- JUDY: Update codeblock above once you have the complete Response. -->

In het hier getoonde voorbeeld, controleert de gebruiker om de lijst van eigenschappen te zien die in het model voor de activiteit worden gebruikt waarvan identiteitskaart van de Activiteit 260840 is.

![Stap 1](assets/models-api-step-1.png)

>[!NOTE]
>
>Navigeer naar de Activiteitenlijst in het dialoogvenster [!DNL Target] UI. Klik op de activiteit van belang. De activiteit-id wordt weergegeven in de hoofdtekst van de resulterende pagina Overzicht van activiteiten en aan het einde van de URL voor die pagina.

De **[!UICONTROL externalName]** is een gebruiksvriendelijke naam voor een functie. Het wordt gemaakt door [!DNL Target]en het is mogelijk dat deze waarde in de loop der tijd verandert. Gebruikers kunnen deze gebruikersvriendelijke namen weergeven in het dialoogvenster [Verslag over persoonlijke inzichten](https://experienceleague.adobe.com/docs/target/using/reports/insights/personalization-insights-reports.html).

De **[!UICONTROL internalName]** is de werkelijke id van de functie. Het wordt ook gemaakt door [!DNL Target], maar het kan niet worden gewijzigd. Dit is de waarde waarnaar u moet verwijzen om de functie(s) te identificeren die u wilt lijsten van gewezen personen.

Houd er rekening mee dat de lijst met functies alleen waarden kan bevatten (zodat deze niet null is) als een activiteit:

1. Status = Live hebben of eerder geactiveerd zijn
1. Er moet lang genoeg zijn geweest om campagne-activiteit te kunnen voeren, zodat het model gegevens heeft om tegen te lopen.

## Stap 2: Controleer de lijst van gewezen personen van de activiteit {#step2}

Bekijk nu de lijst van gewezen personen. Met andere woorden, controleer of er functies zijn die momenteel niet in de modellen voor deze activiteit kunnen worden opgenomen.

>[!ERROR]
>
>Let op: `/blockList/` is hoofdlettergevoelig in het verzoek.

>[!BEGINTABS]

>[!TAB Verzoek]

```json {line-numbers="true"}
GET https://mc.adobe.io/<tenant>/target/models/features/blockList/<campaignId>
```

>[!TAB Antwoord]

```json {line-numbers="true"}

```

>[!ENDTABS]

In het hier weergegeven voorbeeld controleert de gebruiker de lijst met geblokkeerde functies voor de activiteit waarvan de activiteit-id 260840 is. De resultaten zijn leeg, wat betekent dat deze activiteit momenteel geen gevoegde op lijst van gewenste personen functies heeft.

![Stap 2](assets/models-api-step-2.png)

>[!NOTE]
>
>U ziet mogelijk lege resultaten zoals deze, de eerste keer dat u de volledige lijst van gewezen personen controleert voordat u er functies aan toevoegt. Als u echter functies uit een lijst van gewezen personen hebt toegevoegd (en vervolgens verwijderd), ziet u mogelijk iets andere resultaten, waarbij een lege, op de lijst met ongewenste personen staan array met functies wordt geretourneerd. Lees verder om een voorbeeld hiervan te bekijken in [Stap 4](#step4).

## Stap 3: voeg eigenschappen aan de lijst van gewezen personen van de activiteit toe {#step3}

Om eigenschappen aan de lijst van gewezen personen toe te voegen, verander het verzoek van GET in PUT, en wijzig het lichaam van het verzoek om te specificeren `blockedFeatureSources` of `blockedFeatures` naar wens.

* De inhoud van het verzoek vereist: `blockedFeatures` of `blockedFeatureSources`. Beide kunnen worden opgenomen.
* Vullen `blockedFeatures` met waarden die zijn geïdentificeerd uit `internalName`. Zie [Stap 1](#step1).
* Vullen `blockedFeatureSources` met waarden uit de onderstaande tabel.

Let op: `blockedFeatureSources` Hiermee wordt aangegeven waar een functie vandaan komt. Voor het voegend op lijst van gewenste personen maken dienen zij als groepen of categorieën eigenschappen, die gebruikers toelaten om volledige reeksen eigenschappen in één keer te blokkeren. De waarden van `blockedFeatureSources` komen overeen met de eerste tekens van de id van een functie (`blockedFeatures` of `internalName` waarden); daarom kunnen ze ook als &quot;voorvoegsels van functies&quot; worden beschouwd.

### Tabel `blockedFeatureSources` waarden {#table}

| Voorvoegsel | Beschrijving |
| --- | --- |
| VAK | Mbox, parameter |
| URL | Aangepast - URL-parameter |
| ENV | Omgeving |
| SES | Bezoekerprofiel |
| GEO | Geo-locatie |
| PRO | Aangepast - profiel |
| SEG | Aangepast - segment rapporteren |
| AAM | Aangepast - Experience Cloud-segment |
| MOB | Mobiel |
| CRS | Aangepast - Klantkenmerken |
| UPA | Aangepast - RT-CDP-profielkenmerk |
| IAC | Belangengebieden bezoekers |  |

>[!BEGINTABS]

>[!TAB Verzoek]

```json {line-numbers="true"}
PUT https://mc.adobe.io/<tenant>/target/models/features/blockList/<campaignId>

{
    "blockedFeatureSources": ["AAM"],
    "blockedFeatures": ["SES_PREVIOUS_VISIT_COUNT", "SES_TOTAL_SESSIONS"]
}
```

>[!TAB Antwoord]

```json {line-numbers="true"}
{
    "blockedFeatures": [
            "SES_PREVIOUS_VISIT_COUNT",
            "SES_TOTAL_SESSIONS"
        ],
    "blockedFeatureSources": [
            "AAM"
        ]
}
```

>[!ENDTABS]

In het hier weergegeven voorbeeld blokkeert de gebruiker twee functies. `SES_PREVIOUS_VISIT_COUNT` en `SES_TOTAL_SESSIONS`, die zij eerder hebben geïdentificeerd door de volledige lijst met functies te vragen voor de activiteit waarvan activiteit-id 260480 is, zoals beschreven in [Stap 1](#step1). Zij blokkeren ook alle eigenschappen die uit de Segmenten van Experience Cloud komen, die door eigenschappen met de prefix van &quot;AAM,&quot;worden bereikt te blokkeren zoals die in [table](#table) hierboven.

![Stap 3](assets/models-api-step-3.png)

Nadat u een functie hebt gevoegd op lijst van gewenste personen, wordt u aangeraden de bijgewerkte lijst van gewezen personen te controleren door [Stap 2](#step2) nogmaals (GET de lijst van gewezen personen). Controleer of de resultaten er goed uitzien (controleer of de resultaten de functies bevatten die zijn toegevoegd uit de meest recente aanvraag voor PUT).

## Stap 4: (Optioneel) Blokkeren opheffen {#step4}

Als u alle op de lijst met ongewenste personen staan functies wilt ontgrendelen, wist u de waarden uit `blockedFeatureSources` of `blockedFeatures`.

>[!BEGINTABS]

>[!TAB Verzoek]

```json {line-numbers="true"}
PUT https://mc.adobe.io/<tenant>/target/models/features/blockList/<campaignId>

{
    "blockedFeatureSources": [],
    "blockedFeatures": []
}
```

>[!TAB Antwoord]

```json {line-numbers="true"}
{
    "blockedFeatures": [],
    "blockedFeatureSources": []
}
```

>[!ENDTABS]

In het hier getoonde voorbeeld, ontruimt de gebruiker hun lijst van gewezen personen voor de activiteit waarvan identiteitskaart van de Activiteit 260840 is. In het antwoord worden lege arrays voor zowel geblokkeerde functies als hun bronnen bevestigd—`blockedFeatureSources` en `blockedFeatures`, respectievelijk.

![Stap 4](assets/models-api-step-4.png)

Zoals altijd, na het wijzigen van de lijst van gewezen personen, adviseert men dat u uitvoert [Stap 2](#step2) nogmaals (GET de lijst van gewezen personen om te verifiëren de lijst eigenschappen zoals verwacht omvat). In het hier weergegeven voorbeeld controleert de gebruiker of zijn lijst van gewezen personen nu leeg is.

![Stap 4b](assets/models-api-step-4b.png)

Vraag: Hoe kan ik sommige, maar niet alle, lijsten van gewezen personen verwijderen?

Antwoord: Om een discrete ondergroep van op de lijst met ongewenste personen staan eigenschappen uit een multi-eigenschapslijst van gewezen personen te verwijderen, kunnen de gebruikers eenvoudig de bijgewerkte lijst van eigenschappen verzenden zij binnen willen blokkeren [het verzoek om lijst van gewezen personen](#step3)in plaats van de hele lijst van gewezen personen te wissen en de gewenste functies opnieuw toe te voegen. Met andere woorden, verzend de bijgewerkte eigenschaplijst (zoals aangetoond in [Stap 3](#step3)), waarbij u ervoor zorgt dat de functies die u wilt verwijderen, niet in de lijst van gewezen personen worden opgenomen.

## Stap 5: (Optioneel) Beheer de algemene lijst van gewezen personen {#step5}

De bovenstaande voorbeelden hadden allemaal betrekking op één enkele activiteit. U kunt eigenschappen voor alle activiteiten over een bepaalde cliënt (huurder) ook blokkeren, in plaats van het moeten de lijst van gewezen personen voor elke activiteit afzonderlijk specificeren. Als u een algemene lijst van gewezen personen wilt uitvoeren, gebruikt u de `/blockList/global` vraag, in plaats van `blockList/<campaignId>`.

>[!BEGINTABS]

>[!TAB Verzoek]

```json {line-numbers="true"}
PUT https://mc.adobe.io/<tenant>/target/models/features/blockList/global

{
    "blockedFeatureSources": ["AAM", "PRO", "ENV"],
    "blockedFeatures": ["AAM_FEATURE_1", "AAM_FEATURE_2"]
}
```

>[!TAB Antwoord]

```json {line-numbers="true"}
{
    "blockedFeatures": [
        "AAM_FEATURE_1",
        "AAM_FEATURE_2"
    ],
    "blockedFeatureSources": [
        "AAM",
        "PRO",
        "ENV"
    ]
}
```

>[!ENDTABS]

In het voorbeeldVerzoek hierboven wordt getoond, blokkeert de gebruiker twee eigenschappen, &quot;AAM_FEATURE_1&quot;en &quot;AAM_FEATURE_2,&quot;voor alle activiteiten in hun [!DNL Target] account. Dit betekent dat, ongeacht de activiteit, &quot;AAM_FEATURE_1&quot; en &quot;AAM_FEATURE_2&quot; niet in de machine het leren modellen voor deze rekening zullen worden omvat. Bovendien blokkeert de gebruiker wereldwijd ook alle functies waarvan het voorvoegsel &quot;AAM&quot;, &quot;PRO&quot; of &quot;ENV&quot; is.

Vraag: Is het bovenstaande codevoorbeeld niet overbodig?

Antwoord: Ja. Het is overtollig om eigenschappen met waarden te blokkeren die met &quot;AAM beginnen,&quot;terwijl ook het blokkeren van alle eigenschappen de waarvan bron &quot;AAM is.&quot; Het nettoresultaat is dat alle functies die afkomstig zijn van AAM (Experience Cloud-segmenten) worden geblokkeerd. Daarom als het doel is alle eigenschappen van de Segmenten van Experience Cloud te blokkeren, individueel specificerend bepaalde eigenschappen die met &quot;AAM&quot;beginnen is onnodig, in het bovenstaande voorbeeld.

Laatste stap: Of dit nu op het niveau van de activiteit of wereldwijd is, u wordt aangeraden de lijst van gewezen personen te verifiëren nadat u deze hebt gewijzigd, om er zeker van te zijn dat deze de waarden bevat die u verwacht. Doe dit door de `PUT` een `GET`.

Hieronder wordt een voorbeeldreactie weergegeven [!DNL Target] blokkeert twee afzonderlijke functies, plus alle functies van &quot;AAM&quot;, &quot;PRO&quot; en &quot;ENV&quot;.

![Stap 5](assets/models-api-step-5.png)
