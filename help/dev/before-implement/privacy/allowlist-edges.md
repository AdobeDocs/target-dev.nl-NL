---
keywords: implementeren, implementeren, whitelist, witte lijst, lijst van gewenste personen, lijst van gewenste personen, edge, edges, $9
description: Bekijk een lijst van gastheren om u te helpen lijst van gewenste personen  [!DNL Adobe Target]  randen (geografisch verdeelde het dienen knopen die optimale reactietijden eind - gebruikers verzekeren).
title: Hoe Voegt op lijst van gewenste personen ik  [!DNL Target]  de Knooppunten van Edge?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 1583cfe8ea1009fd1df5c5a0e5f3f95f72daf2b9
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Lijst van gewenste personen [!DNL Target] randknooppunten

Informatie en een bijgewerkte lijst met hosts om u te helpen de randen van [!DNL Adobe Target] te lijsten van gewenste personen.

Een rand is een geografisch verspreide serverende architectuur die optimale reactietijden voor eindgebruikers verzekert die om inhoud verzoeken, ongeacht waar zij worden gevestigd. Elk Edge-knooppunt heeft alle informatie die nodig is om te reageren op de aanvraag van de inhoud van de gebruiker en om analysegegevens over die aanvraag bij te houden. Gebruikersverzoeken worden naar het dichtstbijzijnde randknooppunt gerouteerd. Voor meer informatie, zie [ het randnetwerk ](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934).

U kunt indien gewenst randknooppunten van [!DNL Target] lijsten van gewenste personen.

>[!IMPORTANT]
>
>Naast het voegend op lijst van gewenste personen de IP van de Vertaling van het Adres van het Netwerk (NATIONAAL) adressen van [!DNL Target] randen en [!DNL Target] randIP adressen die in het artikel worden besproken, zou u alle [!DNL Adobe Analytics] IP adresblokken ook moeten lijsten van gewenste personen.
>
>Voor meer informatie, zie [ Alle het adresblokken van Adobe Analytics IP ](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=en#all-adobe-analytics-ip-address-blocks) {target=_blank} in de *technische nota&#39;s van Adobe Analytics* documentatie.
>
>[!DNL Adobe Target] wordt de infrastructuur bijgewerkt en de klanten die adressen willen lijsten van gewenste personen moeten beide reeksen IPs gebruiken. Het nalaten om dit te doen zal klanten gebruikend server-kant of hybride implementaties beïnvloeden waar de vraag van doel API voor het halen van ervaringen uit binnen een netwerk achter een firewall voortkomt die wordt gevormd om een lijst van gewenste personen te gebruiken.
>
>Alle Edge4 *x* adressen die in beide hieronder lijsten worden vermeld zijn gepland om op 9 augustus 2023 worden bijgewerkt.

## IP-adressen (NAT) van [!DNL Target] randen van netwerkadressen

Lijst met IP-adressen van egress-randen van [!DNL Target] . Lijst van gewenste personen deze IPs als u van plan bent om [!DNL Target] bereik aan uw diensten te hebben.

| Edge-locatie | IP van de uitgang Adressen |
| --- | --- |
| Edge41 (Mumbai) | 3.6.2.221<P>13 235 112,4 <P>52 66 66 192 |
| Edge42 (Tokio) | 52 69 55 232<P>43.206.61.43 <P>13 113 73 214 |
| Edge44 (East Coast US) | 54 164 192 223<P>52.86.86.2003 <P>54 88 167 98 |
| Edge45 (West Coast US) | 52 40 124 129<P>54 148 219,69 <P>54 189 208 212 |
| Edge46 (Sydney) | 54 253 144,4<P>54 66 198 142 <P>13 211 218 51 |
| Edge47 (Ierland) | 52 208 136 136<P>54 170 28 19 <P>99 80 111 82 |
| Edge48 (Singapore) | 3.1.141,36<P>18 143 112 116 <P>52 76 61 44 |

## [!DNL Target] Edge IP-adressen

Lijst met IP-adressen van [!DNL Target] randen. Lijst van gewenste personen deze IPs als u API vraag aan [!DNL Target] randen wilt maken.

Deze lijst wordt vaak gewijzigd, omdat de taakverdelingsmechanisme op basis van verkeersprofielen wordt vergroot en verkleind.

| Edge-locatie | Domein | IP-adressen |
| --- | --- | --- |
|  | `CLIENTCODE.tt.omtrdc.net`<br /> (waarbij CLIENTCODE uw [!DNL Target] client-id is) |  |
| Edge41 (Mumbai) | `mboxedge41.tt.omtrdc.net` | 3.6.2.221<P>52 66 66 192<P>13 235 112,4 |
| Edge42 (Tokio) | `mboxedge42.tt.omtrdc.net` | 43.206.61.43<P>13 113 73 214<P>52 69 55 232 |
| Edge44 (East Coast US) | `mboxedge44.tt.omtrdc.net` | 54 88 167 98<P>54 164 192 223<P>52.86.86.2003 |
| Edge45 (West Coast US) | `mboxedge45.tt.omtrdc.net` | 52 40 124 129<P>54 148 219,69<P>54 189 208 212 |
| Edge46 (Sydney) | `mboxedge46.tt.omtrdc.net` | 54 66 198 142<P>54 253 144,4<P>13 211 218 51 |
| Edge47 (Ierland) | `mboxedge47.tt.omtrdc.net` | 54 170 28 19<P>52 208 136 136<P>99 80 111 82 |
| Edge48 (Singapore) | `mboxedge48.tt.omtrdc.net` | 52 76 61 44<P>3.1.141,36<P>18 143 112 116 |

Wanneer de taakverdelingsmechanisme wijzigingen in het verkeersprofiel detecteert, wordt het vergroot of verkleind. De tijd die nodig is voor de Elastic Load Balancing om te schalen, kan variëren van 1 tot 7 minuten, afhankelijk van de gedetecteerde wijzigingen. Wanneer de ladingsbalanceringen schrapen, werken zij het DNS verslag met de nieuwe lijst van IP adressen bij. Om ervoor te zorgen dat u van de verhoogde capaciteit voordeel haalt, gebruikt het Elastic Tassen die een TL plaatsen op het DNS verslag van 60 seconden plaatst.
