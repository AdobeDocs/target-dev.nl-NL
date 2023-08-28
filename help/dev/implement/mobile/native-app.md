---
keywords: mobiele app,aep-sdk,native app,webweergaven,native;swift,adobe-ervaren platform voor mobiele sdk,mobiele sdk,native code
description: Leer hoe u implementeert [!DNL Adobe Target] met de [!DNL AEP Mobile SDK] in een native app met webweergaven.
title: Implementeren [!DNL Adobe Target] in een mobiele toepassing die native code gebruikt met webweergaven
feature: Implement Mobile
role: Developer
source-git-commit: c0fda36cb5472d71438c47b8b484716003da4214
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---


# Implementeren [!DNL Target] met de [!DNL AEP Mobile SDK] in een native app met webweergaven

In dit artikel worden de beste praktijken voor de implementatie van [!DNL Adobe Target] in een mobiele toepassing die native code gebruikt met webweergaven die de [!DNL Adobe Experience Platform Mobile SDK].

In dit artikel wordt een voorbeeld van een iOS-toepassing gebruikt met de [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/getting-started/){target=_blank} and a [!DNL Target] integration written in [Swift from the GitHub repository](https://github.com/adobe/aep-sdk-app/){target=_blank}.

In de echte wereld gebruikt uw onderneming-app waarschijnlijk webweergaven in uw mobiele app. Een webweergave is een container die een webpagina laadt met een URL. De container is vergelijkbaar met een browservenster zonder besturingselementen. In iOS werkt de webweergavecontainer als een Safari-browser bij het verwerken van webpagina&#39;s.

## Vereisten

Ga als volgt te werk: [!DNL Adobe Experience Platform Mobile SDK], moet u bepaalde taken uitvoeren die aan de voorwaarde voldoen.

Zie voor meer informatie [Adobe Target](https://developer.adobe.com/client-sdks/documentation/adobe-target/){target=_blank} in the [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/){target=_blank} documentatie.

## Native code synchroniseren met webweergaven

De uitdaging bij de implementatie [!DNL Target] in een native app met webweergaven is het zo dat [!DNL Adobe Experience Platform Mobile SDK] al alle vereiste id&#39;s heeft gegenereerd voor [!DNL Adobe] oplossingen die naadloos werken. De id&#39;s zijn echter nog niet zichtbaar voor de webweergaven omdat deze id&#39;s zich niet in de native platformomgeving bevinden. Daarom moet u een brug tot stand brengen om sommige herkenningstekens van SDK tot de Webmeningen over te gaan zodat de bezoekersidentiteit in het Webmilieu voortduurt. Als u dit niet doet, worden er dubbele bezoeken afgelegd, wat van invloed is op uw rapportage.

Gelukkig [!DNL Adobe Experience Platform Mobile SDK] biedt een handige methode om te genereren [!DNL Adobe] parameters die vereist zijn voor webweergaven om te gebruiken en door te gaan voor dezelfde bezoeker, zoals getoond in de volgende voorbeeldcode:

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  print("appendedURL \(String(describing: appendedURL))")
  // load the url with ECID on the main thread
  DispatchQueue.main.async {
    let request = NSMutableURLRequest(url: appendedURL!)
    self.webView.load(request as URLRequest)
  }
});
```

Voor meer informatie over de `Identity.appendTo` en om een voorbeeld te zien van hoe u de methode kunt gebruiken, raadpleegt u [Swift > Voorbeeld](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/tabs/api-reference/){target=_blank} in de *Mobiele SDK-documentatie*.

Gebruiken `Identity.appendTo`, deze URL:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2
```

transformeert naar:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg
```

Zoals u kunt zien, is er `adobe_mc` parameter toegevoegd aan de URL. Deze parameter bevat gecodeerde waarden voor:

* TS=1660667205: Het huidige tijdstempel. Dit tijdstempel zorgt ervoor dat de webweergave geen verlopen waarden ontvangt.
* MCMID=69624092487065093697422606480535692677: De [!UICONTROL Experience Cloud ID] (ECID). Ook bekend als MID of [!UICONTROL Marketing Cloud ID] vereist voor [!DNL Adobe] identificatie van bezoekers voor verschillende oplossingen.
* MCORGID=EB9CAE8B56E003697F000101@AdobeOrg: De [!UICONTROL Adobe Organization ID].

De `Identity.getUrlVariables` is een alternatief [!DNL Adobe Experience Platform Mobile SDK] methode die een correct gevormde koord terugkeert dat bevat [!DNL Experience Cloud Identity Service] URL-variabelen. Zie voor meer informatie [getUrlVariables](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#geturlvariables){target=_blank} in de *IdentiteitAPI-naslaggids*.

## Geef de [!DNL Target] Sessie-id voor ervaringen van dezelfde sessie

Er is één extra stap nodig om het [!DNL Target] de reis van de gebruiker werkt naadloos over de inheemse en Webmeningen. Deze stap omvat het extraheren en passeren van de [!DNL Target] Sessie-id van de [!DNL Adobe Experience Platform Mobile SDK] in de webweergaven van de mobiele app.

De `Target.getSessionId` extraheert de sessie-id die als een `mboxSession` parameter:

```swift
Target.getSessionId { (id, err) in
    // read Target sessionId
}
```

## Testen in de webweergaven

Webvoorvertoningskoppelingen worden gegenereerd op het tabblad [!UICONTROL Activity detail] pagina door op de knop [[!UICONTROL Adobe QA] link](/help/dev/implement/mobile/target-mobile-preview.md) om een pop-up weer te geven om elke koppeling van de ervaringsvoorvertoning te kopiëren, vergelijkbaar met het volgende:

```
?at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Webvoorvertoningskoppelingen bevatten aanvullende `at_preview_index` en `at_preview_listed_activities_only` parameters. Kopieer deze parameters om mobiele, gebruiksvriendelijke voorvertoningskoppelingen te maken met weblink-parameters.

Bijvoorbeeld:

```
com.adobe.targetmobile://?at_preview_token=mhFIzJSF7JWb-RsnakpBqhBwj-TiIlZsRTx_1QQuiXLIJFdpSLeEZwKGPUyy57O_&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Nadat u de koppeling hebt geopend in een iOS Safari-browser, legt uw app de URL vast in uw `AppDelegate` klasse vergelijkbaar met het volgende voorbeeld:

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
  print("url= \(String(describing: url.absoluteString))")
  //...
```

Nu u alle vereiste parameters in de app hebt vastgelegd, kunt u ze indien nodig aan het web doorgeven:

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  let urlWithWebPreviewLink = appendedURL + "&" + myPreviewLinkFromAppDelegate
```

De uiteindelijke uitvoer voor de webweergavekoppeling kan er als volgt uitzien:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg&at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```
