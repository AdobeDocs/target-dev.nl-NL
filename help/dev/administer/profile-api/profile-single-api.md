---
title: Adobe Target API voor bijwerken van één profiel
description: Leren gebruiken [!DNL Adobe Target] [!UICONTROL Single Profile Update API] om de profielgegevens van één bezoeker te verzenden naar [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
source-git-commit: 6f7d9875e3b73352ead3a55e40a4b2f81f3d4400
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# [!DNL Adobe Target Single Profile Update API]

De [!DNL Adobe Target] [!UICONTROL Single Profile Update API] Hiermee kunt u een profielupdate voor één gebruiker verzenden. De [!UICONTROL Single Profile Update API] en wordt doorgaans gebruikt wanneer een update moet worden uitgevoerd met betrekking tot een transactie die plaatsvindt in een kanaal dat niet is geïmplementeerd [!DNL Target].

De [!UICONTROL Single Profile Update API] is beperkt tot het uitvoeren van 1 miljoen updates in om het even welke het rollen periode van 24 uur. Updates vinden meestal plaats binnen een uur, maar het kan 24 uur duren voordat ze worden gereflecteerd. Als u meer updates moet verzenden of updates moet verwerken in kortere tijdframes, kunt u overwegen updates van transactionele profielen te verzenden via een update aan de clientzijde (voorkeur) of via de [!DNL Adobe Target] server-kant [Leverings-API](/help/dev/implement/delivery-api/overview.md).

De profielparameters in de indeling opgeven `profile.paramName=value`.

Het profiel bijwerken voor een `pcId`, gebruik:

``````
https://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...
``````

Als u het profiel voor een `mbox3rdPartyId`, gebruik:

``````
shell http://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...
``````

De [!UICONTROL Single Profile Update API] is alleen voor updates. Als er niets wordt gevonden, wordt er geen profiel gemaakt.

## Notities

* Parameters en waarden moeten URL-gecodeerd zijn met UTF-8.
* Parameterindeling is `profile.paramName`.
* Niet alle parameterwaarden moeten voor alle pcIds en mbox3rdPartyIds bestaan.
* Parameters en waarden zijn hoofdlettergevoelig.
* Zowel GET als POST worden ondersteund.
* De huidige formaatbeperkingen voor grens zijn 8 KB voor GET en 60 KB voor POST.

## Antwoord

Een voorbeeldreactie voor de bovenstaande verzoeken ziet er als volgt uit:

`trueRequest successfully submitted`

Dit antwoord geeft aan dat het antwoord is verzonden en binnenkort zal worden verwerkt.