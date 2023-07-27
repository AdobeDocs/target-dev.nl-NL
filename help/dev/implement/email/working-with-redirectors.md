---
keywords: Implementatie, mbox.js niet javascript, redirector, kosten per klik, opbrengst per klik
description: Leer hoe u Redirector's kunt gebruiken in e-mailimplementaties, net als bij het gebruik van een box in uw [!DNL Adobe Target] activiteiten.
title: Hoe werk ik met Redirector?
feature: Implement Email
exl-id: 072368ff-9f17-4709-ac2d-c9e1f0d888bb
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# Werken met directeuren

Gebruik een Redirector vergelijkbaar met hoe u een box in uw tests gebruikt.

Redirector wordt gemaakt met een speciale Redirector-URL waarmee een Redirector-box (Redirector) in uw account wordt geladen. Gebruik deze Redirector net zo als hoe u een box in uw tests gebruikt. Verzend de Redirector-URL naar uw advertentienetwerk als doelkoppeling van de advertentie.

Gebruik Redirector om het volgende te doen:

* Houd klikjes bij van uw weergaveadvertenties naar uw site
* Creeer één enkel gecentraliseerd rapport om kliks te volgen om advertenties op veelvoudige ad netwerken te tonen
* Verschillende weergave- en bestemmingen

  Dezelfde banner bijvoorbeeld landt op uw homepage, categoriepagina en productpagina.

* Zoeken naar welke landingspagina de meeste conversies tot gevolg hebben

Zie voor hulp bij het bepalen van de juiste instellingen [Implementaties die niet op JavaScript zijn gebaseerd](/help/dev/implement/email/overview.md).

## Een redirector maken

Voordat u een redirector kunt gebruiken, moet u deze maken.

1. Bepaal de doelvariaties van de advertentie, inclusief het standaarddoel.
1. Maak de Redirector-URL.

   ```
   https://<your_testandtarget_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox
   /​page?mbox=redirectorlink_456
   &mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fusualdestination%2Ehtm
   ```

   * Wanneer `yourclientcode` is de clientcode van uw bedrijf. De clientcode van uw bedrijf is helemaal in kleine letters en heeft geen speciale tekens.

     Uw clientcode is beschikbaar boven aan het dialoogvenster **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** pagina van de [!DNL Target] interface.

   * `redirectorlink_456` Dit is de naam van de Redirector-box die in uw account wordt weergegeven voor gebruik in campagnes en tests.

     Regelaars functioneren anders dan andere vakken, maar worden net zo weergegeven als elke andere box in uw account. Geef de redirector een naam, zodat deze gemakkelijk kan worden onderscheiden van de standaardtekstvakken in uw account.  Als beste praktijken, begin de mbox naam met &quot;redirectorlink&quot;.

   * Wanneer `http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fusualdestination%2Ehtm` is het standaarddoel.

     Dit moet URL gecodeerd zijn en moet een absolute verwijzing zijn. U kunt de [HTML URL-coderingsverwijzing](https://www.w3schools.com/tags/ref_urlencode.asp) om uw URL&#39;s snel te coderen.

   >[!WARNING]
   >
   >Merk op dat u met Redirector aan een risico van Open Redirect Kwetsbaarheid kunt worden blootgesteld. Om het ongeoorloofde gebruik van verbindingen van Redirector door derden te vermijden, adviseert Adobe u &quot;geautoriseerde gastheren&quot;gebruiken om de standaard omleiding URL domeinen te lijsten van gewenste personen. [!DNL Target] gebruikt gastheren aan lijst van gewenste personen domeinen waaraan u redirects wilt toestaan. Zie voor meer informatie [Creeer Lijsten van gewenste personen die gastheren specificeren die worden gemachtigd om mbox vraag te verzenden naar [!DNL Target]](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html#allowlist) in *Gastheren*.

1. Valideer Redirector.
   1. *Beste praktijken van de veiligheid*: Zorg ervoor dat het domein dat in Redirector wordt gebruikt, zoals hierboven vermeld wordt gevoegd op lijst van gewenste personen. Als u een domein gebruikt dat niet gevoegd op lijst van gewenste personen is, zal Adobe om het even welke vraag aan dat domein blokkeren om kwaadwillige acteurs te verhinderen Redirector te gebruiken om aan potentieel kwaadwillige domeinen om te leiden.
   2. Voeg de Redirector-URL in een browser in en vernieuw deze.
   3. Meld u aan bij uw account, vernieuw de keuzelijst en controleer of de nieuwe Redirector als een box wordt weergegeven.
1. Als u verschillende bestemmingen voor één advertentie zult testen, creeer [Omleidingsvoorstellen](https://experienceleague.adobe.com/docs/target/using/experiences/vec/redirect-offer.html) voor elke versie.
1. Maak de campagne.

   Zie [Implementaties die niet op JavaScript zijn gebaseerd](/help/dev/implement/email/overview.md) voor de juiste opstelling om uw doelstellingen te ontmoeten.
1. Voltooi de kwaliteitscontrole op de campagne.

   Een dummypagina maken met een `<a href>` met de Redirector-URL. Voorbeeld:

   ```
   <a href=https://<your_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox/​page?mbox=
   
   redirectorlink_456&mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2F​usualdestination%2Ehtm>
   ```

1. Verifieer dat alle ervaringen, standaardinhoud, en rapporten zoals verwacht op alle browser types, voor al uw milieu&#39;s handelen.

   >[!NOTE]
   >
   >Redirecteurs worden niet ondersteund door Voorvertoning van aanbieding of Bladeren naar box. Voorvertoning vindt direct in een browser plaats. Ook, `mboxDebug` werkt niet met Redirector.

1. Verzend de volledige Redirector-URL naar het advertentienetwerk van uw beeldscherm als de advertentiebestemming.

## Gebruik een redirector om kosten per klik en opbrengst per klik door te geven

Informatie over het gebruiken van redirector om kosten per klik en opbrengst per klik over te gaan.

### Kosten doorgeven per klik

Gebruik een redirector om de kosten per klik door te geven.

>[!NOTE]
>
>De beste praktijk is om de kostprijs te bepalen aan de hand van de **[!UICONTROL Score per visit]** betrokkenheidsmetrisch.

Toevoegen `&mboxPageValue=-value` naar de URL. Noteer de negatieve waarde.

Voorbeeld: voor de 0,10 cent per klik:

```
https://<your_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox/​page?mbox=redirectorlink_456
&mboxPageValue=-0.1&mboxDefault=​https://www.yourcompany.com/usualdestination.htm
```

### Ontvangsten doorgeven per klik

Gebruik een redirector om de opbrengst per klik over te gaan.

>[!NOTE]
>
>De beste praktijk is om de opbrengstwaarde te bepalen gebruikend **[!UICONTROL Score per visit]** betrokkenheidsmetrisch.

Toevoegen `&mboxPageValue=value` naar de URL.

Voorbeeld: voor een opbrengst van 0,10 cent per klik.

```
https://<​your_clientcode>​​​​.tt​​.omtrdc​.net/​​m2/​yourclientcode/​ubox/​​​page?mbox=redirectorlink_456
&mboxPageValue=0.1​&mbox​Default=​​http%3A%2F%2Fwww%2E​yourcompany%2Ecom​%2Fusualdestination%2Ehtm
```
