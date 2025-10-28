---
keywords: implementeren, implementeren, whitelist, witte lijst, lijst van gewenste personen, lijst van gewenste personen, edge, edges, $9
description: Bekijk een lijst van gastheren om u te helpen lijst van gewenste personen  [!DNL Adobe Target]  randen (geografisch verdeelde het dienen knopen die optimale reactietijden eind - gebruikers verzekeren).
title: Hoe Voegt op lijst van gewenste personen ik  [!DNL Target]  de Knooppunten van Edge?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 662d415bc3c216bcd038f07dcaa0fd83f6518690
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Lijst van gewenste personen [!DNL Target] randknooppunten

Informatie en een bijgewerkte lijst met hosts om u te helpen de randen van [!DNL Adobe Target] te lijsten van gewenste personen.

Een rand is een geografisch verspreide serverende architectuur die optimale reactietijden voor eindgebruikers verzekert die om inhoud verzoeken, ongeacht waar zij worden gevestigd. Elk Edge-knooppunt heeft alle informatie die nodig is om te reageren op de aanvraag van de inhoud van de gebruiker en om analysegegevens over die aanvraag bij te houden. Gebruikersverzoeken worden naar het dichtstbijzijnde randknooppunt gerouteerd. Voor meer informatie, zie [&#x200B; het randnetwerk &#x200B;](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html?lang=nl-NL#concept_0AE2ED8E9DE64288A8B30FCBF1040934).

U kunt indien gewenst randknooppunten van [!DNL Target] lijsten van gewenste personen.

>[!IMPORTANT]
>
>Naast het voegend op lijst van gewenste personen de IP van de Vertaling van het Adres van het Netwerk (NATIONAAL) adressen van [!DNL Target] randen en [!DNL Target] randIP adressen die in het artikel worden besproken, zou u alle [!DNL Adobe Analytics] IP adresblokken ook moeten lijsten van gewenste personen.
>
>Voor meer informatie, zie [&#x200B; Alle het adresblokken van Adobe Analytics IP &#x200B;](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=nl-NL#all-adobe-analytics-ip-address-blocks){target=_blank} in de *technische nota&#39;s van Adobe Analytics* documentatie.
>
>[!DNL Adobe Target] wordt de infrastructuur bijgewerkt en de klanten die adressen willen lijsten van gewenste personen moeten beide reeksen IPs gebruiken. Het nalaten om dit te doen zal klanten gebruikend server-kant of hybride implementaties beïnvloeden waar de vraag van doel API voor het halen van ervaringen uit binnen een netwerk achter een firewall voortkomt die wordt gevormd om een lijst van gewenste personen te gebruiken.

Om ononderbroken toegang tot [!DNL Target] door [!DNL Experience Edge Connector] te verzekeren, kunnen de klanten hun netwerkconfiguraties bijwerken om verkeer aan de volmachtsdienst toe te staan.

## Overzicht van proxyservice

* **Eindpunt van de Dienst**: `https://tnt-web-proxy.adobe.io`.
* **Infrastructuur**: Gehost op het [!DNL Adobe] platform van Ethos.
* **Nota**: Deze dienst gebruikt op latentie-gebaseerde DNS het verpletteren en baseert zich niet op statische IP adressen.

## CNAME-doelen

De volmachtsdienst leidt dynamisch verkeer over veelvoudige gebieden gebruikend CNAME verslagen. Dit zijn de huidige doelstellingen:

| Edge-locatie | IP van de uitgang Adressen |
| --- | --- |
| Regio | CNAME-doel |
| Europa (EU-west-1) | `ethos.pub.ethos11-prod-nld2.ethos.adobe.net` |
| US East (VS-oost-2) | `ethos.pub.ethos11-prod-va7.ethos.adobe.net` |
| US East (VS-oost-1) | `ethos.pub.ethos11-prod-aus5.ethos.adobe.net` |

## Aanbevolen items voor lijst van gewenste personen

Om betrouwbare connectiviteit te verzekeren, lijst van gewenste personen de volgende hostnames:

* `ethos.pub.ethos11-prod-nld2.ethos.adobe.net`
* `ethos.pub.ethos11-prod-va7.ethos.adobe.net`
* `ethos.pub.ethos11-prod-aus5.ethos.adobe.net`

## Optioneel: IP-detectie

Als uw netwerkbeleid op IP-Gebaseerde voegende op lijst van gewenste personen vereist, kunt u de huidige openbare IP adressen bekijken verbonden aan de volmachtsdienst gebruikend dit hulpmiddel:

* `DNSChecker – A Record Lookup for tnt-web-proxy.adobe.io`