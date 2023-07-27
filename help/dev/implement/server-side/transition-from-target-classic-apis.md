---
keywords: api, adobe i/o, classic, adobe developer console
description: Leer hoe u een overgang kunt maken van de [!DNL Adobe Target Classic] API's aan de [!DNL Target] API's op de [!DNL Adobe Developer Console].
title: Hoe ga ik over van [!DNL Target Classic] API's naar [!DNL Target] API's op de [!DNL Adobe Developer Console]?
feature: APIs/SDKs
exl-id: b84e3767-89ad-4e2d-9bb4-7e31bffbc285
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Overgang van [!DNL Target Classic] API&#39;s naar [!DNL Target] API&#39;s op de [!DNL Adobe Developer Console]

Informatie die u helpt bij de overgang van de [!DNL Target Classic] API&#39;s aan de [!DNL Target] API&#39;s op de [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home).

Met de ontmanteling van [!DNL Adobe Target Classic], de API&#39;s die zijn verbonden met uw [!DNL Target Classic] de rekening is ook niet beschikbaar gesteld. Dit artikel helpt u bij de overgang van uw [!DNL Target Classic] API-gebaseerde integratie in de [!DNL Target] API&#39;s die door de [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home).

Voor meer informatie over [!DNL Target] API&#39;s, zie [[!DNL Target] API&#39;s](/help/dev/before-administer/target-api-overview.md). Voor meer informatie over [!DNL Target] SDK&#39;s, zie [[!DNL Target] Implementatie op de server](/help/dev/implement/server-side/server-side-overview.md)

## Terminologie

| Term | Beschrijving |
|--- |--- |
| Klassieke API | API&#39;s die zijn gekoppeld aan uw [!DNL Target Classic] account. Deze API-aanroepen zijn gebaseerd op een gebruikersbenaming en op een wachtwoord gebaseerde verificatie en gebruiken de hostnaam `testandtarget.omniture.com`. Als uw API-aanroepen een gebruikersnaam en wachtwoord bevatten in de aanvraag-URL, moet u de overgang naar de [!DNL Adobe Developer Console] API&#39;s. |
| [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home) | De [!DNL Adobe Developer Console] is de gateway voor [!DNL Target] API&#39;s. Deze API&#39;s zijn verbonden met uw [!DNL Target Standard/Premium] account. De [!DNL Target] API&#39;s op de [!DNL Adobe Developer Console] een [Op JWT gebaseerde verificatie](../../before-administer/configure-authentication.md), de industriestandaard voor veilige bedrijf-API&#39;s. |

## Tijdlijn

De volgende API&#39;s zijn uit bedrijf genomen toen [!DNL Target Classic] is ontmanteld:

| Datum | Details |
|--- |--- |
| 17 oktober 2017 | Alle API-methoden die een schrijfbewerking uitvoeren (`saveCampaign`, `copyCampaign`, `saveHTMLOfferContent`, en `setCampaignState`) zijn buiten bedrijf gesteld.<P>Dit is dezelfde datum als alle [!DNL Target Classic] gebruikersaccounts zijn ingesteld op de status Alleen-lezen. |
| 14 november 2017 | De overige API&#39;s zijn uit bedrijf genomen. Dit is de datum waarop [!DNL Target Classic] gebruikersinterface is uitgeschakeld |

[!DNL Recommendations Classic] API&#39;s zijn niet beïnvloed door deze tijdlijn.

## Gelijkwaardige methoden

In de volgende tabel wordt het equivalent weergegeven [!DNL Adobe Developer Console] API-methoden voor de klassieke API-methoden. De [!DNL Adobe Developer Console] API&#39;s retourneren JSON, terwijl de klassieke API&#39;s XML retourneren.

De [!DNL Adobe Developer Console] API-methoden zijn gekoppeld aan de corresponderende sectie in de API-documentatiesite. Voor elke API-methode wordt een voorbeeld gegeven. U kunt ook de opdracht [!DNL Target] Admin API Postman Collection die steekproefAPI vraag voor alle Adobe API methodes op bevat [!DNL Adobe Developer Console].

| Groepering | Klassieke API-methode | [!DNL Adobe Developer Console] API-methode | Notities |
|--- |--- |--- |--- |
| Campagne/activiteit | Campagne maken | [AB-activiteit maken](https://developers.adobetarget.com/api/#create-ab-activity)<P>[XT-activiteit maken](https://developers.adobetarget.com/api/#create-xt-activity) | De nieuwe APIs verstrekt afzonderlijke creeert methodes voor AB en XT |
|  | Campagne bijwerken | [AB-activiteit bijwerken](https://developers.adobetarget.com/api/#update-ab-activity)<P>[XT-activiteit bijwerken](https://developers.adobetarget.com/api/#update-xt-activity) |  |
|  | Campagne kopiëren | NVT | De API&#39;s voor het maken van activiteiten gebruiken |
|  | Lijst met campagnes | [Lijstactiviteiten](https://developers.adobetarget.com/api/#list-activities) |  |
|  | Campagnestaat | [Activiteitenstatus bijwerken](https://developers.adobetarget.com/api/#update-activity-state) |  |
|  | Campagneweergave | [AB-activiteit ophalen op id](https://developers.adobetarget.com/api/#get-ab-activity-by-id)<P>[XT-activiteit ophalen op id](https://developers.adobetarget.com/api/#get-xt-activity-by-id) |  |
|  | Campagne-id van derden | NVT | Als u een id van een andere leverancier gebruikt, kunnen de relevante activiteitsmethoden worden gebruikt |
| Aanbiedingen | Voorstel maken | [Voorstel maken](https://developers.adobetarget.com/api/#create-offer) |  |
|  | Voorstel ophalen | [Voorstel ophalen op ID](https://developers.adobetarget.com/api/#get-offer-by-id) |  |
|  | Aanbiedingslijst | [Aanbiedingen aanbieden](https://developers.adobetarget.com/api/#list-offers) |  |
|  | Maplijst | NVT | Mappen worden niet ondersteund in [!DNL Target Standard/Premium] |
| Rapportage | Rapport Campagneprestaties | [AB-prestatierapport ophalen](https://developers.adobetarget.com/api/#get-ab-performance-report)<P>[XT-prestatierapport ophalen](https://developers.adobetarget.com/api/#get-xt-performance-report) |  |
|  | Controleverslag | [Controlerapport ophalen](https://developers.adobetarget.com/api/#get-audit-report) |  |
|  | 1-1 Inhoudsrapport | [AP-prestatierapport ophalen](https://developers.adobetarget.com/api/#get-ap-activity-performance-report) |  |
| Accountinstellingen | Hostgroepen ophalen | [Omgevingen weergeven](https://developers.adobetarget.com/api/#list-environments) |  |

## Uitzonderingen

Neem contact op met de succesmanager van de klant als u een uitzondering nodig hebt.

## Help

Neem contact op met [!DNL Adobe Target Client Care] (tt-support@adobe.com) als u vragen hebt of hulp nodig hebt bij het overschakelen van de klassieke API&#39;s naar de [!DNL Target] API&#39;s op de [!DNL Adobe Developer Console].
