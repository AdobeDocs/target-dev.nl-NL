---
keywords: flikkering, at.js, implementatie, asynchroon, asynchroon, synchroon, synchroon, $8
description: Meer informatie over [!DNL Target] voorkomt dat er tijdens het laden van de pagina of de app flikkering optreedt (standaardinhoud wordt tijdelijk weergegeven voordat deze wordt vervangen door activiteit-inhoud).
title: Hoe beheert at.js Flicker?
feature: at.js
exl-id: 8aacf254-ec3d-4831-89bb-db7f163b3869
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 0%

---

# Hoe at.js flikkering beheert

Informatie over hoe de [!DNL Adobe Target] JavaScript-bibliotheek at.js voorkomt flikkering tijdens het laden van de pagina of de toepassing.

Er wordt geflikkerd als de standaardinhoud tijdelijk aan bezoekers wordt weergegeven voordat deze wordt vervangen door de inhoud van de activiteit. flikkering is ongewenst, omdat dit verwarrend kan zijn voor bezoekers.

## Een automatisch gemaakte globale mbox gebruiken

Als u de optie [Globale box automatisch maken](/help/dev/implement/client-side/atjs/global-mbox/customize-global-mbox.md) Als u instelt bij het configureren van at.js, beheert at.js flikkering door de instelling voor dekking te wijzigen terwijl de pagina wordt geladen. Wanneer at.js laadt, wijzigt dit de dekkingsinstelling van het gereedschap `<body>` element aan &quot;0&quot;, waardoor de pagina aanvankelijk onzichtbaar wordt voor bezoekers. Na een reactie van [!DNL Target] ontvangen is, of als er een fout met de [!DNL Target] request is detection—at.js stelt dekking terug naar &quot;1&quot;. Zo weet u zeker dat de bezoeker de pagina alleen ziet nadat de inhoud van uw activiteiten is toegepast.

Als u de instelling inschakelt tijdens het configureren van at.js, stelt at.js de dekking van de HTML BODY-stijl in op 0. Na een reactie van [!DNL Target] wordt ontvangen, stelt bij.js de dekking van HTML BODY opnieuw in op 1.

Dekking ingesteld op 0 houdt de pagina-inhoud verborgen om flikkering te voorkomen, maar de browser geeft de pagina nog steeds weer en laadt alle benodigde elementen, zoals CSS, afbeeldingen, enz.

Indien `opacity: 0` werkt niet in uw implementatie, kunt u flikkering ook beheren door `bodyHiddenStyle` en stel deze in op `body {visibility:hidden !important}`. U kunt beide `body {opacity:0 !important}` of `body {visibility:hidden !important}`, afhankelijk van wat het beste werkt voor uw specifieke omstandigheid.

De volgende illustratie toont het Lichaam van de Huid en toont de vraag van het Lichaam in allebei at.js 1.*x* en at.js 2.x.

**at.js 2.x**

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![Doelstroom: pagina.js laden verzoek](/help/dev/implement/client-side/assets/atjs-20-flow-page-load-request.png "Doelstroom: pagina.js laden verzoek"){zoomable="yes"}

**te.js 1.*x***

(Klik op de afbeelding om deze uit te breiden naar de volledige breedte.)

![Doelstroom: automatisch gemaakt algemeen mbox](/help/dev/implement/client-side/atjs/how-atjs-works/assets/target-flow2.png "doelstroom: automatisch gemaakt algemeen mbox"){zoomable="yes"}

Voor meer informatie over de `bodyHiddenStyle` override, zie [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

## flikkering beheren bij asynchroon laden bij .js

Het asynchroon laden bij.js is een goede manier om te voorkomen dat de browser wordt geblokkeerd bij het renderen. Deze techniek kan echter leiden tot flikkering op de webpagina.

U kunt flikkering voorkomen door een vooraf verborgen fragment te gebruiken dat zichtbaar zal zijn nadat de relevante HTML-elementen door Doel zijn gepersonaliseerd.

at.js kan asynchroon worden geladen, rechtstreeks ingesloten op de pagina of via een tagbeheer (bijvoorbeeld Adobe Experience Platform Launch).

Als at.js op de pagina is ingesloten, moet het fragment worden toegevoegd voordat u at.js laadt. Als u at.js laadt via een tagmanager die ook asynchroon wordt geladen, moet u het fragment toevoegen voordat u het tagbeheer laadt. Als de tagmanager synchroon wordt geladen, kan het script vóór at.js worden opgenomen in de tagmanager.

Het vooraf verborgen codefragment ziet er als volgt uit:

```
;(function(win, doc, style, timeout) {
  var STYLE_ID = 'at-body-style';

  function getParent() {
    return doc.getElementsByTagName('head')[0];
  }

  function addStyle(parent, id, def) {
    if (!parent) {
      return;
    }

    var style = doc.createElement('style');
    style.id = id;
    style.innerHTML = def;
    parent.appendChild(style);
  }

  function removeStyle(parent, id) {
    if (!parent) {
      return;
    }

    var style = doc.getElementById(id);

    if (!style) {
      return;
    }

    parent.removeChild(style);
  }

  addStyle(getParent(), STYLE_ID, style);
  setTimeout(function() {
    removeStyle(getParent(), STYLE_ID);
  }, timeout);
}(window, document, "body {opacity: 0 !important}", 3000));
```

Standaard wordt in het fragment de hele HTML-BODY vooraf verborgen. In sommige gevallen is het verstandig alleen bepaalde HTML-elementen vooraf te verbergen en niet de hele pagina. U kunt dit bereiken door de stijlparameter aan te passen. Het kan worden vervangen door iets dat slechts bepaalde gebieden van de pagina vooraf verbergt.

U hebt bijvoorbeeld twee gebieden die worden aangeduid met ID&#39;s container-1 en container-2, en de stijl kan vervolgens worden vervangen door:

```
#container-1, #container-2 {opacity: 0 !important}
```

In plaats van de standaardinstelling:

```
body {opacity: 0 !important}
```

## Flicker beheren in at.js 2.x voor triggerView()

Wanneer u `triggerView()` om de gerichte inhoud in uw SPA te tonen, wordt het flikkerbeheer verstrekt uit de doos. Dit betekent dat vooraf verborgen logica niet handmatig hoeft te worden toegevoegd. In plaats daarvan verbergt at at.js 2.x de locatie waar de weergave moet worden weergegeven voordat de doelinhoud wordt toegepast.

## Flicker beheren met getOffer() en applyOffer()

Omdat beide `getOffer()` en `applyOffer()` Bij API&#39;s op laag niveau is er geen ingebouwde flikkerbesturing. U kunt een kiezer of HTML-element als optie aan `applyOffer()`in dit geval `applyOffer()` voegt de inhoud van de activiteit aan dit bepaalde element toe; nochtans, moet u ervoor zorgen het element behoorlijk vóór het aanhalen van `getOffer()` en `applyOffer()`.

```
document.documentElement.style.opacity = "0";
 
adobe.target.getOffer({
    mbox: 'target-global-mbox',
    success: function(offer) {
        adobe.target.applyOffer({
            mbox: 'target-global-mbox',
            offer: offer
        });
 
        document.documentElement.style.opacity = "1";
    },
    error: function() {
        document.documentElement.style.opacity = "1";        
    }
});
```

## Een regionale box met mboxCreate() gebruiken in at.js 1.x (niet ondersteund in at.js 2.x)

Als u een regionale mbox-implementatie gebruikt, kunt u `mboxCreate()` met de pagina die u hebt ingericht, lijkt op de volgende voorbeeldcode:

```
<div class="mboxDefault">
Some default content
</div>
<script>
mboxCreate('some-mbox');
</script>
```

Als uw pagina&#39;s correct zijn ingericht, beheert at.js flikkering door de CSS &quot;zicht&quot;bezit van het element met de mboxDefault klasse geschikt te schakelen.
