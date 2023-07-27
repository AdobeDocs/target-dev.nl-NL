---
keywords: custom events, at.js, request failed, request failed, content rendering failed, content rendering failed, library loaded, request start, content rendering start, content rendering no aanbiedingen, content rendering redirect, custom events2
description: Aangepaste gebeurtenissen gebruiken voor de [!DNL Adobe Target] op.js JavaScript-bibliotheek die op de hoogte moet worden gesteld wanneer een aanvraag of aanbieding voor een box mislukt of slaagt.
title: Hoe gebruik ik aangepaste gebeurtenissen at.js?
feature: at.js
exl-id: a4baed9a-9eb8-4343-9834-709b03e44ca2
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# at.js, aangepaste gebeurtenissen

Informatie over `at.js custom events`, die u laat weten wanneer een mbox-aanvraag of -aanbieding mislukt of slaagt.

Historisch gezien heeft mbox.js (nu afgekeurd) andere JavaScript-code die op de pagina wordt uitgevoerd, niet laten weten wat er achter de schermen gebeurt. Met de vooruitgang van om.js, hadden wij een unieke kans om deze kwestie op te lossen.

Volgens onze klanten zijn er verschillende scenario&#39;s waarvan zij op de hoogte willen worden gesteld, zoals:

* Een mbox-aanvraag is mislukt als gevolg van een time-out, onjuiste statuscode, JSON-parseringsfout, enz.
* Een mbox-verzoek is uitgevoerd.
* Rendering van voorstel is mislukt omdat het element wrapping mbox ontbreekt, de kiezer niet is gevonden, enz.
* Rendering van aanbieding is gelukt. DOM-wijzigingen zijn toegepast.

Vooraf gedefinieerde gebeurtenissen hebben een structuur waarmee u de vereiste gegevens kunt extraheren op basis van het gebeurtenistype.

Om ervoor te zorgen dat gebeurtenissen in verschillende scenario&#39;s kunnen worden gebruikt, hebben de douanegebeurtenissen een ladingsvoorwerp dat aan het detailbezit van het gebeurtenisvoorwerp (dat wordt overgegaan tot de manager) wordt toegewezen. Ook om te voorkomen dat tekenreeksen worden doorgegeven als gebeurtenisnamen, worden de gebeurtenissen als constanten weergegeven met `adobe.target.event` naamruimte.

## Structuur

| Sleutel | Type | Beschrijving |
|--- |--- |--- |
| type | String | Er zijn verscheidene scenario&#39;s waarin u om in het vinden, het zuiveren, en het aanpassen van interactie met at.js zou willen worden meegedeeld te helpen.<p>Elke aangepaste gebeurtenis die hieronder wordt vermeld, heeft twee indelingen: een &quot;constante&quot; en een &quot;tekenreekswaarde&quot;.<ul><li>**Constanten**: Voorbereid met `adobe.target.event.`, in kapitalen wordt weergegeven en onderstrepingstekens bevat. Abonneren op aangepaste gebeurtenissen *na* at.js laadt, maar *voor* Wanneer de mbox-reactie is ontvangen, gebruikt u de constante.</li><li>**Tekenreekswaarden**: Kleine letters en bevatten streepjes. Abonneren op aangepaste gebeurtenissen *voor* at.js laadt, gebruik de koordwaarde.</li></ul>**Verzoek is mislukt**<p>Constante: `adobe.target.event.REQUEST_FAILED`<p>Reekswaarde: `at-request-failed`<p>Beschrijving: Een aanvraag voor een box is mislukt als gevolg van een time-out, onjuiste statuscode, JSON-parseringsfout, enz.<p>**Verzoek is uitgevoerd**<p>Constante: `adobe.target.event.REQUEST_SUCCEEDED`<p>Tekenreekswaarde: `at-request-succeeded`<p>Omschrijving: een postaanvraag is geslaagd.<p>**Renderen van inhoud mislukt**<p>Constante: `adobe.target.event.CONTENT_RENDERING_FAILED`<p>Tekenreekswaarde: `at-content-rendering-failed`<p>Beschrijving: Rendering van voorstel is mislukt omdat het element wrapping box ontbreekt, de kiezer niet is gevonden, enz.<p>**Renderen van inhoud gelukt**<p>Constante: `adobe.target.event.CONTENT_RENDERING_SUCCEEDED`<p>Tekenreekswaarde: `at-content-rendering-succeeded`<p>Omschrijving: de rendering van voorstellen is gelukt. DOM-wijzigingen zijn toegepast.<p>**Bibliotheek geladen**<p>Constante: `adobe.target.event.LIBRARY_LOADED`<p>Tekenreekswaarde: `at-library-loaded`<p>Beschrijving: deze gebeurtenis is ideaal om te volgen wanneer at.js volledig is geladen. Met deze gebeurtenis kunt u de uitvoering van het globale selectievakje aanpassen. U kunt deze gebeurtenis ook gebruiken om de globale mbox onbruikbaar te maken en dan naar deze gebeurtenis te luisteren om globale mbox later te branden.<p>**Verzoek starten**<p>Constante: `adobe.target.event.REQUEST_START`<p>Tekenreekswaarde: `at-request-start`<p>Beschrijving: deze gebeurtenis wordt geactiveerd voordat een HTTP-aanvraag wordt uitgevoerd. U kunt deze gebeurtenis voor prestatiemetingen gebruiken gebruikend het Middel Timing API.<p>**Begin van weergave van inhoud**<p>Constante: `adobe.target.event.CONTENT_RENDERING_START`<p>Tekenreekswaarde: `at-content-rendering-start`<p>Beschrijving: deze gebeurtenis wordt geactiveerd voordat de kiezersopiniepeiling wordt gestart en inhoud naar de pagina wordt gerenderd. U kunt deze gebeurtenis gebruiken om de voortgang van de rendering van inhoud bij te houden.<p>**Inhoud renderen geen aanbiedingen**<p>Constante: `adobe.target.event.CONTENT_RENDERING_NO_OFFERS`<p>Tekenreekswaarde: `at-content-rendering-no-offers`<p>Beschrijving: deze gebeurtenis wordt geactiveerd wanneer er geen voorstellen worden geretourneerd.<p>**Omleiding van weergave van inhoud**<p>Constante: `adobe.target.event.CONTENT_RENDERING_REDIRECT`<p>Tekenreekswaarde: `at-content-rendering-redirect`<p>Beschrijving: deze gebeurtenis wordt geactiveerd wanneer een aanbieding een omleiding is en [!DNL Target] wordt doorgestuurd naar een andere URL. |
| mbox | String | naam van mbox |
| message | String | Bevat een beschrijving die leesbaar is voor mensen, zoals wat er is gebeurd, het foutbericht, enzovoort. |
| bijhouden | Object | Bevat de `sessionId` en `deviceId`. In sommige gevallen `deviceId` kan ontbreken omdat [!DNL Target] kan het bestand niet ophalen van de Edge-server. |
| type | String | **Artefact voor apparaatbeslissingen is geslaagd**<p>Constante:<p>`adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`<p>Reekswaarde: `artifactDownloadSucceeded`<p>Beschrijving: Wordt opgeroepen wanneer het doelwit van de beslissing op het apparaat is gedownload.<p>**Artefact voor apparaatbesluitvorming is mislukt**<p>Constante: `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`<p>Tekenreekswaarde: `artifactDownloadFailed`<p>Beschrijving: Wordt opgeroepen wanneer het beslissingsartefact op het apparaat niet kan worden gedownload. |

## Gebruik

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(event) { 
  console.log('Event', event); 
});
```

## Trainingsvideo: respontokens en de aangepaste gebeurtenissen at.js ![Zelfstudie-badge](../../../assets/tutorial.png)

Bekijk de volgende video om te leren hoe u de Tokens van de Reactie en Aangepaste gebeurtenissen at.js kunt gebruiken om profielgegevens te delen van [!DNL Target] op systemen van derden.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)
