---
title: Adobe Target API-overzicht
description: Overzicht van de verschillende Adobe Target API's, waaronder de API voor levering, api voor rapportage, api voor beheerders, api voor profielen, api voor aanbevelingen en koppelingen naar postmanverzamelingen.
exl-id: bf886103-36af-4061-b8be-2fe645f45ff3
feature: APIs/SDKs
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Overzicht doelAPI

In dit artikel worden de verschillende doel-API&#39;s in het algemeen beschreven voordat u zich richt op specifieke vereisten voor de API&#39;s Admin en Profile. Als u Doel via de gebruikersinterface wilt beheren, raadpleegt u de [rubriek van de *Adobe Target Business User Guide*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=nl-NL).

## API-typen

De Adobe Target API&#39;s zijn een verzameling API&#39;s die Adobe Target-producten, zoals Adobe Recommendations, van stroom voorzien. Met deze API&#39;s kunt u gegevensrijke gebruikersinterfaces maken die u kunt gebruiken om gegevens te manipuleren en te integreren.

Adobe Target API&#39;s kunnen worden gegroepeerd op type: Admin, Profile, Delivery en Reporting.

>[!NOTE]
>
>De API&#39;s voor beheerders en profiel-API&#39;s worden vaak gezamenlijk genoemd (&quot;Admin en Profile API&#39;s&quot;), maar kunnen ook afzonderlijk worden vermeld (&quot;Admin API&#39;s&quot; en &quot;Profile API&#39;s&quot;). De Recommendations API is een specifieke implementatie van een Target Admin API.

| API-type | Wat het u toelaat doen | Koppeling downloaden | Andere nuttige koppelingen |
| --- | --- | --- |--- |
| [Beheerder](../administer/admin-api/admin-api-overview-new.md) | Maak, wijzig en verwijder activiteiten, publiek, aanbiedingen en andere objecten (waaronder Recommendations-entiteiten, criteria, ontwerpen, enzovoort). De Recommendations API&#39;s zijn een type Admin API.) | <UL><li>[Postman-verzameling voor Admin API](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Recommendations API Postman Collection](https://developer.adobe.com/target/administer/recommendations-api/#section/Postman)</li></UL> | [Recommendations API&#39;s gebruiken](../before-administer/recs-api/overview.md) |
| Profiel | In Adobe Target opgeslagen gebruikersprofielen ophalen en wijzigen. | [Postman-verzameling voor doelprofiel](https://developers.adobetarget.com/api/#profiles) |  |
| [Aflevering](../implement/delivery-api/overview.md) | Haal geoptimaliseerde en gepersonaliseerde inhoud van Target op voor levering aan een eindgebruiker. | [Postman-collectie voor doel-leverings-API](/help/dev/before-implement/delivery-api-overview/getting-started.md#postman) |  |
| [Rapportage](../administer/admin-api/admin-api-overview-new.md) | Resultaten van exportactiviteiten en andere rapportresultaten. | Rapportage-API&#39;s zijn opgenomen in de [Postman-collectie voor Admin API van doel](https://developers.adobetarget.com/api/#admin-postman-collection). |  |
| [Modellen](../administer/models-api/models-api-overview.md) | Beheer de lijst met functies die door Target zijn uitgesloten van de modellen voor machinaal leren (de lijst van gewezen personen). De API Modellen is een type Admin API, maar wordt hier afzonderlijk vermeld vanwege de unieke bewerkingen tegen objecten (lijsten van gewezen personen) die niet toegankelijk zijn via de interface. |  |  |

## API-verschillen

Er is een belangrijk onderscheid tussen API&#39;s voor doelbeheer (inclusief de Recommendations API&#39;s) en API&#39;s voor doellevering:

* Admin APIs laat u diverse aspecten van Doel vormen die u in het Doel UI kunt ook vormen. De uitzondering op dit is Modellen API, die u aspecten van Doel laat vormen niet beschikbaar in UI. Ongeacht de instelling **voor alle Admin API&#39;s is verificatie vereist.**

* Met levering-API&#39;s kunt u inhoud ophalen. Voor levering-API&#39;s is geen verificatie vereist.

Als u API&#39;s voor doelbeheer wilt gebruiken, moet u verificatie configureren met de [Adobe Developer Console](https://developer.adobe.com/console/home). Zie voor meer informatie [Verificatie configureren](../before-administer/configure-authentication.md).
