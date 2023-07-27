---
keywords: implementeren, implementeren, implementeren, adobe launch, lanceren, ras, omleiden, ervaren platform launch, platform launch, tags, adobe platform, implementeren2
description: Leer hoe u de [!DNL Adobe Target] at.js-bibliotheek gebruiken [!DNL Adobe Experience Platform], de voorkeursmethode voor de implementatie van Target.
title: Hoe implementeren [!DNL Target] gebruiken [!DNL Adobe Experience Platform]?
feature: Implement Server-side
exl-id: 0a325871-194a-479c-a3bf-294e3dde3e9a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Implementeren [!DNL Target] gebruiken [!DNL Adobe Experience Platform]

Tags in [!DNL Adobe Experience Platform] zijn de volgende generatie mogelijkheden voor tagbeheer van [!DNL Adobe]. Met labels kunnen klanten op een eenvoudige manier de analytische, marketing- en advertentietags implementeren en beheren die nodig zijn om relevante klantervaringen mogelijk te maken.

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in [!DNL Adobe Experience Platform]. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?) voor een geconsolideerde referentie van de terminologische wijzigingen.

In de volgende tabel worden de verschillende bronnen weergegeven waar u meer informatie kunt vinden:

| Bron | Details |
|--- |--- |
| [Adobe Target toevoegen](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/target.html#implement-solutions) | Deze zelfstudie bevat stapsgewijze instructies voor het implementeren [!DNL Target] in een website met tags in [!DNL Adobe Experience Platform]. Tot de onderwerpen behoren het toevoegen van de JavaScript-bibliotheek at.js, het afvuren van de globale box, het toevoegen van parameters en het integreren met andere oplossingen. Dit artikel maakt deel uit van een grotere zelfstudie die u laat zien hoe u Adobe Experience Platform en andere Adobe Experience Cloud-oplossingen implementeert. |
| [Snelstartgids](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html) | Informatie over het opstellen van en het beheren van de analytische, marketing, en reclame markeringen noodzakelijk om relevante klantenervaringen te aandrijven. |
| [Adobe [!DNL Target] extensieoverzicht](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html) | Informatie over de uitvoering [!DNL Target] gebruiken [!DNL Adobe Experience Platform]. |

## Voordelen van de implementatie van at.js met behulp van de [!DNL Target] extension

De volgende voordelen zijn alleen van toepassing als u tags gebruikt in [!DNL Adobe Experience Platform] om te implementeren in.js. Om deze reden stelt Adobe sterk voor om tags te gebruiken in [!DNL Adobe Experience Platform] in plaats van een handmatige implementatie van at.js.

* **Solven [!DNL Adobe Analytics] en [!DNL Target] rasvoorwaarde:** Omdat de [!DNL Analytics] de vraag kon vóór worden in brand gestoken [!DNL Target] de [!DNL Target] aanroep is niet gekoppeld aan de [!DNL Analytics] vraag. Deze opeenvolging kan tot onjuiste gegevens leiden. De [!DNL Target] zorgt ervoor dat de [!DNL Analytics] de bakenvraag wacht tot [!DNL Target] de vraag voltooit, met succes of niet. Tags gebruiken in [!DNL Adobe Experience Platform] lost de gegevensinconsistentie op klanten kunnen ervaren wanneer manueel het uitvoeren.

  >[!NOTE]
  >
  >Gebruik de actie Send Beacon in het dialoogvenster [!DNL Adobe Analytics] zodat de [!DNL Analytics] de vraag wacht op [!DNL Target] vraag. Als u rechtstreeks `s.t()` of `s.tl()` aangepaste code gebruiken, [!DNL Analytics] vraag wacht niet tot [!DNL Target] de vraag is volledig.

* **Voorkomt onjuiste omleiding van aanbiedingen:** Als u [!DNL Target] en [!DNL Analytics] op de pagina, en er is een omleidingsaanbod uitgevoerd door Target, kunt u een situatie ervaren waarin [!DNL Analytics] tracker voert een aanvraag in als dat niet zou mogen (omdat de gebruiker wordt omgeleid naar een andere URL). Als u [!DNL Target] en [!DNL Analytics] via tags in [!DNL Adobe Experience Platform], zult u dit probleem niet ervaren. Tags gebruiken in [!DNL Adobe Experience Platform], [!DNL Target] instructies [!DNL Analytics] om de [!DNL Analytics] baken-verzoek.
