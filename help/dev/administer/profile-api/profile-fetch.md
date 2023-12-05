---
title: Ophaalprofielen
description: Leer hoe u API's met Adobe Target Profile kunt gebruiken om bezoekersgegevens op te halen die u kunt gebruiken in [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
source-git-commit: e5a1c38d448cb7446b7b26cd0dc882976ba94dd3
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# Profielen bijwerken

A [!DNL Target] profiel kan op twee manieren worden opgehaald: met een `tntid` of `thirdPartyId`.

## Een titer gebruiken

[!DNL Target] wijst automatisch een `tntid` voor elk verzoek.

In het volgende voorbeeld wordt de aanvraagindeling getoond om een profiel op te halen met een `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/your-tnt-id?client=<your-client-code>
```

Vervangen `<your-client-code>` en `your-tnt-id` en een verzoek om GET in werking te stellen. Hier is een vraag van de het halen van het voorbeeldprofiel gebruikend een `tntid`;

```
http://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/111492025094307-353046?client=<your-client-code>
```

## Een derdePartyId gebruiken

[!DNL Adobe Target] profielen kunnen worden aangevuld met uw eigen id (bijvoorbeeld: CRM-id, `uuid`, lidmaatschapsnummer enzovoort).

Zie [Profielen bijwerken](/help/dev/administer/profile-api/profile-api-overview.md) om te leren hoe u een `thirdPartyId` naar uw profiel.

In het volgende voorbeeld wordt de aanvraagindeling getoond om een profiel op te halen met een `thirdPartyId`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/your-thirdpartyid?client=<your-client-code>
```

Vervangen `<your-client-code>` en `your-thirdpartyid` en een verzoek om GET in werking te stellen. Hier is een vraag van de het halen van het voorbeeldprofiel gebruikend een [!UICONTROL thirdpartyid]:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/a1-mbox3rdPartyId?client=<your-client-code>
```

Wanneer deze vraag wordt gemaakt, [!DNL Target] pogingen om het profiel eerst te vinden in de cluster die in de randaanvraag is vermeld, of waar het profiel zich bevindt en de inhoud te retourneren. De inhoud van het profiel wordt geretourneerd in de JSON-indeling.

## Verificatie

De [!DNL Target Profile API] kan worden beveiligd door verificatie in te schakelen vanaf de [!DNL Target] UI zoals hier beschreven. Nadat de verificatie is ingeschakeld, moeten voor alle API-profielaanvragen het token voor profielverificatie is ingesteld in de aanvraagheaders. Het token zelf kan worden gegenereerd met het [!DNL Target] UI of het gebruiken van de stappen hierboven in [Token voor profielverificatie](https://developers.adobetarget.com/api/#authentication-tokens){target=_blank} sectie.

## Metering

Deze vraag telt niet op uw mbox vraag.

## Foutafhandeling

In geval van een oproep tot `/thirdPartyId` met een ongeldige of een verlopen `thirdPartyId` gespecificeerd:

```
{"status" : 404, "message" : "No profile found for client <client_code> with third party id=<third_party_id>"}
```

Als het profiel niet kan worden gevonden of is verlopen:

```
{"status" : 404, "message" : "No profile found for client <client_code> with mboxPC=<mbox_pc>"}
```
