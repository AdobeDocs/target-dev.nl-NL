---
keywords: implementatie, api, profiel, API-instellingen voor profielen, verificatietoken
description: Leer hoe u verificatie voor batchupdates configureert via [!DNL Adobe Target] API's en genereren een profielverificatietoken.
title: Hoe gebruik ik profiel-API-instellingen om batchupdates in of uit te schakelen?
feature: APIs/SDKs
exl-id: 968f33d0-296b-4248-8c9a-8e6f3077bdfa
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# Profiel-API-instellingen

Verificatie voor batchupdates in- of uitschakelen via [!DNL Adobe Target] API&#39;s en genereren een profielverificatietoken.

[!DNL Adobe Target] maakt en onderhoudt een profiel voor elke individuele gebruiker. Dit profiel is opgeslagen op het tabblad [!DNL Target] edge-cluster en wordt na elk bezoek in real-time bijgewerkt. U kunt een profiel ook afzonderlijk of in bulk bijwerken via API.

Voor extra veiligheid, kunt u vereisen dat de Bulk API vraag van de Update een geldig toegangstoken wordt overgegaan in de kopbal van het verzoek.

**Om authentificatie te vereisen en een toegangstoken te produceren gebruikend [!DNL Target] UI:**

1. Klik op **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.
1. Onder **[!UICONTROL Profile API]** schuiven **[!UICONTROL Require Authentication]** schakelen naar de in- of uitgeschakeld positie.

   ![alternatieve afbeelding](assets/profile_api_settings.png)

1. (Voorwaardelijk) Als u vereiste voor verificatie hebt ingeschakeld, klikt u op **[!UICONTROL Generate New Profile Authentication Token]**.

   ![alternatieve afbeelding](assets/profile_api_settings_2.png)

   Het token verloopt volgens de tijd die in het vak Verloopt in wordt vermeld.

   U moet een van de volgende gebruikersmachtigingen hebben om een verificatietoken te genereren:

   * Beheerdersrol of hebben ten minste rechten van fiatteurs

     Voor meer informatie voor de Standaardklanten van het Doel, zie [Rollen en machtigingen opgeven](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions) in *Gebruikers*. Voor meer informatie voor [!DNL Target Premium] klanten, zie [Bedrijfsmachtigingen configureren](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

   * Beheerdersrol op het niveau van de werkruimte/het productprofiel

     Werkruimten zijn beschikbaar voor [!DNL Target Premium] alleen aan klanten. Zie voor meer informatie [Bedrijfsmachtigingen configureren](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

   * Admin Rights (bevoegdheid Sysadmin) op de [!DNL Adobe Target] productniveau

U kunt ook een profielverificatietoken genereren via de API. Zie &quot;Profielen&quot; in het dialoogvenster [Handleiding Adobe Target Admin en Profile API](../../administer/admin-api/admin-api-overview-new.md).

1. Kopieer het token en neem het op in de koptekst van het verzoek met de notatie &quot;Autorisatie&quot; : &quot;Drager&quot;.

1. Klikken **[!UICONTROL Generate New Profile Authentication Token]** om het token zo nodig opnieuw te genereren.

>[!WARNING]
>
>Als u dit token opnieuw instelt, mislukken API-aanroepen met het huidige token. Hiervoor moeten alle scripts of apps die deze token gebruiken, worden bijgewerkt.
