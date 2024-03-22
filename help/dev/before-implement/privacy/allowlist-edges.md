---
keywords: implementeren, implementeren, whitelist, witte lijst, lijst van gewenste personen, lijst van gewenste personen, edge, edges, $9
description: Een lijst met hosts weergeven om u te helpen lijsten van gewenste personen [!DNL Adobe Target] randen (geografisch verdeelde het dienen knopen die optimale reactietijden eind - gebruikers verzekeren).
title: Hoe kan ik Lijsten van gewenste personen? [!DNL Target] Randknooppunten?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 49b6572c0d414ab304712691c97794bb0b1e3781
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Lijst van gewenste personen [!DNL Target] Edge-knooppunten

Informatie en een bijgewerkte lijst van gastheren om u te helpen lijsten van gewenste personen [!DNL Adobe Target] randen.

Een rand is een geografisch verspreide serverende architectuur die optimale reactietijden voor eindgebruikers verzekert die om inhoud verzoeken, ongeacht waar zij worden gevestigd. Elk Edge-knooppunt heeft alle informatie die nodig is om te reageren op de aanvraag van de inhoud van de gebruiker en om analysegegevens over die aanvraag bij te houden. Gebruikersverzoeken worden naar het dichtstbijzijnde randknooppunt gerouteerd. Zie voor meer informatie [Het Edge-netwerk](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934).

U kunt lijst van gewenste personen [!DNL Target] randknooppunten, indien gewenst.

>[!IMPORTANT]
>
>Naast het voegend op lijst van gewenste personen de IP van het Adres van het Netwerk Vertaling (NATIONAAL) adressen van [!DNL Target] randen en [!DNL Target] rand IP adressen die in het artikel worden besproken, zou u ook lijst van gewenste personen allen moeten [!DNL Adobe Analytics] IP-adresblokken.
>
>Zie voor meer informatie [Alle Adobe Analytics IP-adresblokken](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=en#all-adobe-analytics-ip-address-blocks){target=_blank} in de *Adobe Analytics tech notes* documentatie.
>
>[!DNL Adobe Target] de infrastructuur wordt bijgewerkt en de klanten die adressen willen lijsten van gewenste personen moeten beide reeksen IPs gebruiken. Het nalaten om dit te doen zal klanten gebruikend server-kant of hybride implementaties beïnvloeden waar de vraag van doel API voor het halen van ervaringen uit binnen een netwerk achter een firewall voortkomt die wordt gevormd om een lijst van gewenste personen te gebruiken.
>
>Alle Edge4 *x* de adressen die in beide lijsten worden vermeld zijn gepland om op 9 augustus 2023 worden bijgewerkt.

## IP-adressen (NAT) van Network Address Translation [!DNL Target] randen

Lijst met IP-adressen van egress van [!DNL Target] randen. Lijst van gewenste personen deze IPs als u van plan bent te hebben [!DNL Target] richt zich tot uw diensten.

| Locatie rand | IP van de uitgang Adressen |
| --- | --- |
| Edge41 (Mumbai) | 3.6.2.221<br />13 235 112,4 <br />52 66 66 192 |
| Edge42 (Tokio) | 52 69 55 232<br />43.206.61.43 <br />13 113 73 214 |
| Edge44 (East Coast US) | 54 164 192 223<br />52.86.86.2003 <br />54 88 167 98 |
| Edge45 (West Coast US) | 52 40 124 129<br />54 148 219,69 <br />54 189 208 212 |
| Edge46 (Sydney) | 54 253 144,4<br />54 66 198 142 <br />13 211 218 51 |
| Edge47 (Ierland) | 52 208 136 136<br />54 170 28 19 <br />99 80 111 82 |
| Edge48 (Singapore) | 3.1.141,36<br />18 143 112 116 <br />52 76 61 44 |

## [!DNL Target] edge IP-adressen

Lijst met IP-adressen van [!DNL Target] randen. Lijst van gewenste personen deze IPs als u API vraag wilt maken aan [!DNL Target] randen.

Deze lijst wordt vaak gewijzigd, omdat de taakverdelingsmechanisme op basis van verkeersprofielen wordt vergroot en verkleind.

| Locatie rand | Domein | IP-adressen |
| --- | --- | --- |
|  | `CLIENTCODE.tt.omtrdc.net`<br />(waarbij CLIENTCODE uw [!DNL Target] client-id) |  |
| Edge41 (Mumbai) | `mboxedge41.tt.omtrdc.net` | 15.206.104,6<br />3 109 14 178 <br />13 234 139 131 |
| Edge42 (Tokio) | `mboxedge42.tt.omtrdc.net` | 52 194 84 34<br />3 115 158,39 <br />18 180 123 21 |
| Edge44 (East Coast US) | `mboxedge44.tt.omtrdc.net` | 54 205 210,54<br />23.20.189,8 <br />35 169 173 155 |
| Edge45 (West Coast US) | `mboxedge45.tt.omtrdc.net` | 35 161 163,45<br />44 230 114 101 <br />35 161 120 22 |
| Edge46 (Sydney) | `mboxedge46.tt.omtrdc.net` | 3 104 142 61<br />52 62 4 152 <br />54 253 105 140 |
| Edge47 (Ierland) | `mboxedge47.tt.omtrdc.net` | 18.203.168.186<br />54 228 83 91 <br />54 217 181,83 |
| Edge48 (Singapore) | `mboxedge48.tt.omtrdc.net` | 54 179 670<br />13 215 150 94 <br />18 136 47 70 |

Wanneer de taakverdelingsmechanisme wijzigingen in het verkeersprofiel detecteert, wordt het vergroot of verkleind. De tijd die nodig is voor de Elastic Load Balancing om te schalen, kan variëren van 1 tot 7 minuten, afhankelijk van de gedetecteerde wijzigingen. Wanneer de ladingsbalanceringen schrapen, werken zij het DNS verslag met de nieuwe lijst van IP adressen bij. Om ervoor te zorgen dat u van de verhoogde capaciteit voordeel haalt, gebruikt het Elastic Tassen die een TL plaatsen op het DNS verslag van 60 seconden plaatst.
