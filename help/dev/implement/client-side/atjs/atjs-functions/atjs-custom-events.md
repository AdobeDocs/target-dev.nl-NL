---
keywords: custom events, at.js, request failed, request failed, content rendering failed, content rendering failed, library loaded, request start, content rendering start, content rendering no aanbiedingen, content rendering redirect, custom events2
description: De douanegebeurtenissen van het gebruik voor de { [!DNL Adobe Target]  at.js JavaScript bibliotheek die moeten worden op de hoogte gebracht wanneer een mbox verzoek of een aanbieding ontbreekt of slaagt.
title: Hoe gebruik ik aangepaste gebeurtenissen at.js?
feature: at.js
exl-id: a4baed9a-9eb8-4343-9834-709b03e44ca2
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# at.js, aangepaste gebeurtenissen

Informatie over `at.js custom events` , waarmee u kunt zien wanneer een aanvraag of aanbieding voor een box mislukt of slaagt.

Historisch gezien, liet mbox.js (nu afgekeurd) andere code van JavaScript die op de pagina loopt niet weten wat achter de scènes gebeurt. Met de vooruitgang van om.js, hadden wij een unieke kans om deze kwestie op te lossen.

Volgens onze klanten zijn er verschillende scenario&#39;s waarvan zij op de hoogte willen worden gesteld, zoals:

* Een mbox-aanvraag is mislukt als gevolg van een time-out, onjuiste statuscode, JSON-parseringsfout, enz.
* Een mbox-verzoek is uitgevoerd.
* Rendering van voorstel is mislukt omdat het element wrapping mbox ontbreekt, de kiezer niet is gevonden, enz.
* Rendering van aanbieding is gelukt. DOM-wijzigingen zijn toegepast.

Vooraf gedefinieerde gebeurtenissen hebben een structuur waarmee u de vereiste gegevens kunt extraheren op basis van het gebeurtenistype.

Om ervoor te zorgen dat gebeurtenissen in verschillende scenario&#39;s kunnen worden gebruikt, hebben de douanegebeurtenissen een ladingsvoorwerp dat aan het detailbezit van het gebeurtenisvoorwerp (dat wordt overgegaan tot de manager) wordt toegewezen. Wanneer u wilt voorkomen dat tekenreeksen worden doorgegeven als naam van een gebeurtenis, worden de gebeurtenissen als constanten weergegeven met behulp van `adobe.target.event` namespace.

## Structuur

| Sleutel | Type | Beschrijving |
|--- |--- |--- |
| type | String | Er zijn verscheidene scenario&#39;s waarin u om in het vinden, het zuiveren, en het aanpassen van interactie met at.js zou willen worden meegedeeld te helpen.<p>Elke aangepaste gebeurtenis die hieronder wordt vermeld, heeft twee indelingen: een &quot;constante&quot; en een &quot;tekenreekswaarde&quot;.<ul><li>**Constanten**: Voorgewerkt met `adobe.target.event.`, die in alle kapitalen worden voorgesteld, en bevatten onderstrepingstekens. Om aan douanegebeurtenissen in te tekenen *na* at.js laadt maar *alvorens* de mbox reactie is ontvangen, gebruik de constante.</li><li>**Waarden van het Koord**: In kleine letters en bevatten streepjes. Om aan douanegebeurtenissen in te tekenen *vóór* at.js laadt, gebruik de koordwaarde.</li></ul>**Ontbroken Verzoek**<p>Constante: `adobe.target.event.REQUEST_FAILED`<p>Tekenreekswaarde: `at-request-failed`<p>Beschrijving: Een aanvraag voor een box is mislukt als gevolg van een time-out, onjuiste statuscode, JSON-parseringsfout, enz.<p>**Verzoek succesvol**<p>Constante: `adobe.target.event.REQUEST_SUCCEEDED`<p>Tekenreekswaarde: `at-request-succeeded`<p>Omschrijving: een postaanvraag is geslaagd.<p>**Inhoud teruggeven ontbrak**<p>Constante: `adobe.target.event.CONTENT_RENDERING_FAILED`<p>Tekenreekswaarde: `at-content-rendering-failed`<p>Beschrijving: Rendering van voorstel is mislukt omdat het element wrapping box ontbreekt, de kiezer niet is gevonden, enz.<p>**Inhoud die succesvol teruggeeft**<p>Constante: `adobe.target.event.CONTENT_RENDERING_SUCCEEDED`<p>Tekenreekswaarde: `at-content-rendering-succeeded`<p>Omschrijving: de rendering van voorstellen is gelukt. DOM-wijzigingen zijn toegepast.<p>**Geladen Bibliotheek**<p>Constante: `adobe.target.event.LIBRARY_LOADED`<p>Tekenreekswaarde: `at-library-loaded`<p>Beschrijving: deze gebeurtenis is ideaal om te volgen wanneer at.js volledig is geladen. Met deze gebeurtenis kunt u de uitvoering van het globale selectievakje aanpassen. U kunt deze gebeurtenis ook gebruiken om de globale mbox onbruikbaar te maken en dan naar deze gebeurtenis te luisteren om globale mbox later te branden.<p>**Begin van het Verzoek**<p>Constante: `adobe.target.event.REQUEST_START`<p>Tekenreekswaarde: `at-request-start`<p>Beschrijving: deze gebeurtenis wordt geactiveerd voordat een HTTP-aanvraag wordt uitgevoerd. U kunt deze gebeurtenis voor prestatiemetingen gebruiken gebruikend het Middel Timing API.<p>**Inhoud die Begin teruggeven**<p>Constante: `adobe.target.event.CONTENT_RENDERING_START`<p>Tekenreekswaarde: `at-content-rendering-start`<p>Beschrijving: deze gebeurtenis wordt geactiveerd voordat de kiezersopiniepeiling wordt gestart en inhoud naar de pagina wordt gerenderd. U kunt deze gebeurtenis gebruiken om de voortgang van de rendering van inhoud bij te houden.<p>**Inhoud die geen Aanbiedingen teruggeeft**<p>Constante: `adobe.target.event.CONTENT_RENDERING_NO_OFFERS`<p>Tekenreekswaarde: `at-content-rendering-no-offers`<p>Beschrijving: deze gebeurtenis wordt geactiveerd wanneer er geen voorstellen worden geretourneerd.<p>**Inhoud die Redirect teruggeeft**<p>Constante: `adobe.target.event.CONTENT_RENDERING_REDIRECT`<p>Tekenreekswaarde: `at-content-rendering-redirect`<p>Beschrijving: deze gebeurtenis wordt geactiveerd wanneer een aanbieding een omleiding is en [!DNL Target] wordt omgeleid naar een andere URL. |
| mbox | String | naam van mbox |
| message | String | Bevat een beschrijving die leesbaar is voor mensen, zoals wat er is gebeurd, het foutbericht, enzovoort. |
| bijhouden | Object | Bevat de `sessionId` en `deviceId` . In sommige gevallen ontbreekt `deviceId` mogelijk omdat [!DNL Target] het bestand niet kan ophalen van de Edge-server. |
| type | String | **Op apparaat volgde bepalingsartefact**<p>Constante:<p>`adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`<p>Tekenreekswaarde: `artifactDownloadSucceeded`<p>Beschrijving: Wordt opgeroepen wanneer het doelwit van de beslissing op het apparaat is gedownload.<p>**ontbroken het Beslissingsartefact van het apparaat**<p>Constante: `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`<p>Tekenreekswaarde: `artifactDownloadFailed`<p>Beschrijving: Wordt opgeroepen wanneer het beslissingsartefact op het apparaat niet kan worden gedownload. |

## Gebruik

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(event) { 
  console.log('Event', event); 
});
```

## De Video van de opleiding: De Tokens van de Reactie en de Gebeurtenissen van de Douane at.js ![ badge van het Leerprogramma ](../../../assets/tutorial.png)

Bekijk de volgende video om te leren hoe u de Tokens van de Reactie en de Gebeurtenissen van de Douane bij.js kunt gebruiken om profielinformatie van [!DNL Target] aan derdesystemen te delen.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)
