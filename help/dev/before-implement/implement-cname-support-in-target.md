---
keywords: clientverzorging, naam, certificaatprogramma, canonieke naam, cookies, certificaat, amc, door adobe beheerd certificaat, digicert, domeinbesturingsvalidatie, dcv, clientverzorging2
description: Het werk met [!UICONTROL Adobe Client Care] om steun CNAME (Canonical Name) in  [!DNL Adobe Target]  uit te voeren om ad-blokkerende kwesties te behandelen.
title: Hoe gebruik ik CNAME als doel?
feature: Privacy & Security
exl-id: 5709df5b-6c21-4fea-b413-ca2e4912d6cb
source-git-commit: 04dfc34bcd3e7efbf73cd167334b440d42cafd1b
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 0%

---

# CNAME en Doel

Instructies voor het werken met [!DNL Adobe Client Care] om ondersteuning voor CNAME (Canonical Name) te implementeren in [!DNL Adobe Target] . Gebruik CNAME om problemen met of beleid voor ITP-cookies (Intelligent Tracking Prevention) te verwerken en te blokkeren. Met CNAME, worden de vraag gemaakt aan een domein dat door de klant eerder dan een domein wordt bezeten van Adobe.

## Ondersteuning voor CNAME aanvragen in Doel

1. Bepaal de lijst met hostnamen die u nodig hebt voor uw SSL-certificaat (zie de Veelgestelde vragen hieronder).

1. Maak voor elke hostnaam een CNAME-record in de DNS die verwijst naar uw gewone [!DNL Target] hostname `clientcode.tt.omtrdc.net` .

   Als uw clientcode bijvoorbeeld &#39;nameCustom&#39; is en uw voorgestelde hostnaam `target.example.com` is, ziet uw DNS CNAME-record er ongeveer als volgt uit:

   ```
   target.example.com.  IN  CNAME  cnamecustomer.tt.omtrdc.net.
   ```

   >[!WARNING]
   >
   >DigiCert, de certificeringsinstantie van Adobe, kan pas een certificaat uitgeven als deze stap is voltooid. Daarom kan Adobe uw verzoek om een implementatie CNAME niet vervullen tot deze stap volledig is.

1. [ Vul deze vorm ](assets/FPC_Request_Form.xlsx) in en omvat het wanneer u [ een kaartje van de Zorg van de Cliënt van Adobe die de steun van de NAAM verzoekt ](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?lang=nl-NL&#reference_ACA3391A00EF467B87930A450050077C):

   * [!DNL Adobe Target] clientcode:
   * SSL-certificaathostnamen (bijvoorbeeld: `target.example.com target.example.org`):
   * Aankoper van SSL-certificaten (Adobe wordt zeer aanbevolen, zie Veelgestelde vragen): Adobe/klant
   * Als de klant het certificaat aanschaft, ook wel &#39;Create Your Own Certificate&#39; (BYOC) genoemd, voert u de volgende aanvullende gegevens in:
      * Certificaatorganisatie (bijvoorbeeld: Example Company Inc):
      * Organisatorische eenheid certificaat (optioneel, bijvoorbeeld: Marketing):
      * Certificaatland (voorbeeld: VS):
      * Certificaatstatus/regio (bijvoorbeeld: Californië):
      * Plaats van certificaat (voorbeeld: San Jose):

1. Als Adobe het certificaat aanschaft, werkt Adobe samen met DigiCert om uw certificaat aan te schaffen en te implementeren op Adobe-productieservers.

   Als de klant het certificaat (BYOC) aanschaft, verzendt de Clientservice van Adobe u de CSR (Certificate Signing Request). Gebruik de CSR wanneer u het certificaat aanschaft via de gekozen certificeringsinstantie. Nadat het certificaat is uitgegeven, verzendt u een kopie van het certificaat en eventuele tussenliggende certificaten naar de Adobe Client Care voor implementatie.

   Adobe Client Care brengt u op de hoogte wanneer uw implementatie gereed is.

1. Werk `serverDomain` [ documentatie ](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverdomain) aan nieuwe CNAME hostname bij en plaats `overrideMboxEdgeServer` aan `false` [ documentatie ](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#overridemboxedgeserver) in uw configuratie at.js.

## Veelgestelde vragen

De volgende informatie beantwoordt vaak gestelde vragen over het verzoeken van en het uitvoeren van de steun van CNAME in Doel:

### Kan ik mijn eigen certificaat opgeven (breng uw eigen certificaat of BYOC)?

U kunt uw eigen certificaat opgeven. Adobe beveelt deze praktijk echter niet aan. Het beheer van de levenscyclus van het SSL-certificaat is zowel voor Adobe als voor u eenvoudiger als Adobe het certificaat koopt en beheert. SSL-certificaten moeten elk jaar worden vernieuwd. Daarom moet Adobe Client Care elk jaar contact met u opnemen om een nieuw certificaat te verkrijgen. Sommige klanten kunnen moeite hebben om een vernieuwd certificaat tijdig te produceren. De implementatie van [!DNL Target] wordt in gevaar gebracht wanneer het certificaat verloopt omdat browsers geen verbinding maken.

>[!WARNING]
>
>Als u een CNAME-implementatie met een [!DNL Target] bring-your-own-certificate aanvraagt, bent u verantwoordelijk voor het jaarlijks verstrekken van vernieuwde certificaten aan Adobe Client Care. Als u toestaat dat uw CNAME-certificaat verloopt voordat Adobe een vernieuwd certificaat kan implementeren, resulteert dit in een stroomstoring voor uw specifieke [!DNL Target] -implementatie.

### Hoe lang tot mijn nieuwe SSL certificaat verloopt?

Alle door Adobe gekochte certificaten zijn één jaar geldig. Zie {het artikel van 0} DigiCert op 1 jaar certificaten [ voor meer informatie.](https://www.digicert.com/blog/position-on-1-year-certificates)

### Welke hostnames moet ik kiezen? Hoeveel hostnames per domein zou ik moeten kiezen?

De implementaties van CNAME van het doel vereisen slechts één hostname per domein op het SSL certificaat en in DNS van de klant. Adobe raadt één hostnaam per domein aan. Sommige klanten vereisen meer hostnames per domein voor hun eigen doeleinden (bijvoorbeeld het testen in het opvoeren), wat wordt ondersteund.

De meeste klanten kiezen een hostnaam zoals `target.example.com` . Adobe beveelt aan deze praktijk te volgen, maar uiteindelijk is de keuze aan u. Vraag geen hostname van een bestaand DNS verslag aan. Dit veroorzaakt een conflict en vertraagt tijd aan resolutie van uw [!DNL Target] verzoek CNAME.

### Ik heb al een CNAME-implementatie voor Adobe Analytics. Kan ik hetzelfde certificaat of dezelfde hostnaam gebruiken?

Nee, [!DNL Target] vereist een aparte hostnaam en certificaat.

### Heeft mijn huidige implementatie van [!DNL Target] gevolgen voor ITP 2.x?

Apple Intelligent Tracking Prevention (ITP) versie 2.3 introduceerde de CNAME Cloaking Mitigation-functie, waarmee [!DNL Target] CNAME-implementaties kunnen worden gedetecteerd en de vervaldatum van het cookie tot zeven dagen wordt teruggebracht. [!DNL Target] heeft momenteel geen oplossing voor de CNAME-camouflage van ITP. Voor meer informatie over ITP, zie [ Intelligente het Volgen Preventie van Apple (ITP) 2.x ](../before-implement/privacy/apple-itp-2x.md).

### Welk soort de dienstverstoringen kan ik verwachten wanneer mijn implementatie CNAME wordt opgesteld?

Er is geen de dienstverstoring wanneer het certificaat wordt opgesteld (met inbegrip van certificaatvernieuwingen).

Nadat u echter de hostnaam in de [!DNL Target] -implementatiecode (`serverDomain` in at.js) hebt gewijzigd in de nieuwe CNAME-hostnaam (`target.example.com` ), behandelen webbrowsers terugkerende bezoekers als nieuwe bezoekers. Het retourneren van bezoekersprofielgegevens gaat verloren omdat het vorige cookie niet toegankelijk is onder de oude hostnaam (`clientcode.tt.omtrdc.net`). De vorige cookie is niet toegankelijk vanwege beveiligingsmodellen van de browser. Deze verstoring komt slechts op de aanvankelijke besnoeiing-over aan nieuwe CNAME voor. Certificaatverlengingen hebben niet hetzelfde effect omdat de hostnaam niet verandert.

### Welk zeer belangrijk type en algoritme van de certificaathandtekening voor mijn implementatie CNAME wordt gebruikt?

Alle certificaten zijn RSA SHA-256 en de sleutels zijn RSA 2048 beetje, door gebrek. Toetsgrootten groter dan 2048 bits moeten expliciet via [!UICONTROL Customer Care] worden aangevraagd.

### Hoe kan ik bevestigen dat mijn implementatie CNAME klaar voor verkeer is?

Gebruik de volgende set opdrachten (in de opdrachtregelterminal van macOS of Linux, met bash en curl >=7.49):

1. Kopieer en plak deze basfunctie in uw terminal, of plak de functie in het bash-opstartscriptbestand (meestal `~/.bash_profile` of `~/.bashrc` ) zodat de functie beschikbaar is in de verschillende eindsessies:

   +++Zie details

   ```
   function adobeTargetCnameValidation {
     local hostname="$1"
   
     if [ -z "$hostname" ]; then
       echo "ERROR: no hostname specified"
       return 1
     fi
   
     local service="Adobe Target CNAME implementation"
     local edges="41 42 44 45 46 47 48"
     local edgeDomain="tt.omtrdc.net"
     local edgeFormat="mboxedge%d%s.$edgeDomain"
     local poolDomain="pool.data.adobedc.net"
     local shards=5
     local shardsFoundCount=0
     local shardsFound=""
     local shardsFoundOutput=""
     local curlRegex="subject:.*CN=|expire date:|issuer:"
     local curlValidation="SSL certificate verify ok"
     local curlResponseValidation='"OK"'
     local curlEndpoint="/uptime?mboxClient=uptime3"
     local url="https://$hostname$curlEndpoint"
     local sslShopperUrl="https://www.sslshopper.com/ssl-checker.html#hostname=$hostname"
     local success="✅"
     local failure="🚫"
     local info="🔎"
     local rule="="
     local horizontalRule="$(seq ${COLUMNS:-30} | xargs printf "$rule%.0s")"
     local miniRule="$(seq 5 | xargs printf "$rule%.0s")"
     local curlVersion="$(curl --version | head -1 | cut -d' ' -f2)"
     local curlVersionRequired=7.49
     local edgeCount="$(wc -w <<< "$edges" | tr -d ' ')"
     local cnameExists=""
     local endToEndTestSucceeded=""
   
     for region in IRL1 IND1 SIN OR SYD VA TYO; do
       local currShard="${region}-${poolDomain}"
       local curlResult="$(curl -vsm20 --connect-to "$hostname:443:$currShard:443" "$url" 2>&1)"
   
       if grep -q "$curlValidation" <<< "$curlResult"; then
         shardsFound+=" $currShard"
   
         if grep -q "$curlResponseValidation" <<< "$curlResult"; then
           shardsFoundCount=$((shardsFoundCount+1))
           shardsFoundOutput+="\n\n$miniRule $success $hostname [edge shard: $currShard] $miniRule\n"
         else
           shardsFoundOutput+="\n\n$miniRule $failure $hostname [edge shard: $currShard] $miniRule\n"
         fi
   
         shardsFoundOutput+="$(grep -E "$curlRegex" <<< "$curlResult" | sort)"
   
         if ! grep -q "$curlResponseValidation" <<< "$curlResult"; then
           shardsFoundOutput+="\nERROR: unexpected HTTP response from this shard using $url"
         fi
       fi
     done
   
     echo
     echo "$horizontalRule"
     echo
     echo "$service validation for hostname $hostname:"
   
     local dnsOutput="$(dig -t CNAME +short "$hostname" 2>&1)"
     if grep -qFi ".$edgeDomain" <<< "$dnsOutput"; then
       echo "$success $hostname passes DNS CNAME validation"
       cnameExists=true
     else
       echo -n "$failure $hostname FAILED DNS CNAME validation -- "
       if [ -n "$dnsOutput" ]; then
         echo -e "$dnsOutput is not in the subdomain $edgeDomain"
       else
         echo "required DNS CNAME record pointing to <target-client-code>.$edgeDomain not found"
       fi
     fi
   
     for region in IRL1 IND1 SIN OR SYD VA TYO; do
       local curlResult="$(curl -vsm20 --connect-to "$hostname:443:${region}-pool.data.adobedc.net:443" "https://$hostname$curlEndpoint" 2>&1)"
   
       if grep -q "$curlValidation" <<< "$curlResult"; then
         if grep -q "$curlResponseValidation" <<< "$curlResult"; then
           echo -en "$success $hostname passes TLS and HTTP response validation for region $region"
           if [ -n "$cnameExists" ]; then
             echo
           else
             echo " -- the DNS CNAME is not pointing to the correct subdomain for ${service}s with Adobe-managed certificates" \
               "(bring-your-own-certificate implementations don't have this requirement), but this test passes as configured"
           fi
           endToEndTestSucceeded=true
         else
           echo -n "$failure $hostname FAILED HTTP response validation for region $region --" \
             "unexpected response from $url -- "
           if [ -n "$cnameExists" ]; then
             echo "DNS is NOT pointing to the correct shard, notify Adobe Client Care"
           else
             echo "the required DNS CNAME record is missing, see above"
           fi
         fi
       else
         echo -n "$failure $hostname FAILED TLS validation for region $region -- "
         if [ -n "$cnameExists" ]; then
           echo "DNS is likely NOT pointing to the correct shard or there's a validation issue with the certificate or" \
             "protocols, see curl output below and optionally SSL Shopper ($sslShopperUrl):"
           echo ""
           echo "$horizontalRule"
           echo "$curlResult" | sed 's/^/    /g'
           echo "$horizontalRule"
           echo ""
         else
           echo "the required DNS CNAME record is missing, see above"
         fi
       fi
     done
   
     if [ "$shardsFoundCount" -ge "$edgeCount" ]; then
       echo -n "$success $hostname passes shard validation for the following $shardsFoundCount edge shards:"
       echo -e "$shardsFoundOutput"
       echo
   
       if [ -n "$cnameExists" ] && [ -n "$endToEndTestSucceeded" ]; then
         echo "$horizontalRule"
         echo ""
         echo "  For additional TLS/SSL validation, see SSL Shopper:"
         echo ""
         echo "    $info  $sslShopperUrl"
         echo ""
         echo "  To check DNS propagation around the world, see whatsmydns.net:"
         echo ""
         echo "    $info  DNS A records:     https://whatsmydns.net/#A/$hostname"
         echo "    $info  DNS CNAME record:  https://whatsmydns.net/#CNAME/$hostname"
       fi
     else
       echo -n "$failure $hostname FAILED shard validation -- shards found: $shardsFoundCount," \
         "expected: $edgeCount"
       echo ""
     fi
   
     echo
     echo "$horizontalRule"
     echo
   }
   ```

   +++

1. Plak deze opdracht (waarbij `target.example.com` wordt vervangen door uw hostnaam):

   ```adobeTargetCnameValidation target.example.com```

   Als de implementatie gereed is, ziet u de uitvoer hieronder. Het belangrijkste onderdeel is dat alle regels voor validatiestatus `✅` in plaats van `🚫` weergeven. Elke Target edge CNAME shard zou `CN=target.example.com` moeten tonen, die primaire hostname op het gevraagde certificaat aanpast (extra SAN hostnames op het certificaat worden niet gedrukt in deze output).

   +++Zie details

   ```
   $ adobeTargetCnameValidation target.example.com
   
   ==========================================================
   
   Adobe Target CNAME implementation validation for hostname target.example.com:
   ✅ target.example.com passes DNS CNAME validation
   ✅ target.example.com passes TLS and HTTP response validation for region IRL1
   ✅ target.example.com passes TLS and HTTP response validation for region IND1
   ✅ target.example.com passes TLS and HTTP response validation for region SIN
   ✅ target.example.com passes TLS and HTTP response validation for region OR
   ✅ target.example.com passes TLS and HTTP response validation for region SYD
   ✅ target.example.com passes TLS and HTTP response validation for region VA
   ✅ target.example.com passes TLS and HTTP response validation for region TYO
   ✅ target.example.com passes shard validation for the following 7 edge shards:
   
   ===== ✅ target.example.com [edge shard: IRL1-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: IND1-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: SIN-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: OR-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: SYD-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: VA-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: TYO-pool.data.adobedc.net] =====
   *  expire date: Feb 20 23:59:59 2026 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ==========================================================  
   
   For additional TLS/SSL validation, see SSL Shopper:
   
       🔎  https://www.sslshopper.com/ssl-checker.html#hostname=target.example.com  
   
   To check DNS propagation around the world, see whatsmydns.net:
   
       🔎  DNS A records:     https://whatsmydns.net/#A/target.example.com
       🔎  DNS CNAME record:  https://whatsmydns.net/#CNAME/target.example.com 
   ```

   +++

>[!NOTE]
>
>Als dit bevestigingsbevel op DNS bevestiging ontbreekt maar u reeds de noodzakelijke DNS veranderingen hebt aangebracht, zou u op uw DNS updates kunnen moeten wachten om volledig te verspreiden. DNS de verslagen hebben bijbehorend [ TTL (tijd-aan-levende) ](https://en.wikipedia.org/wiki/Time_to_live#DNS_records) die geheim voorgeheugenvervaltijd voor DNS antwoorden van die verslagen dicteert. Dientengevolge, zou u minstens zolang uw TTLs kunnen moeten wachten. U kunt het `dig target.example.com` bevel of [ gebruiken Toolbox van de Reeks van G ](https://toolbox.googleapps.com/apps/dig/#CNAME) om uw specifieke TTLs omhoog te kijken. Om DNS propagatie rond de wereld te controleren, zie [ what smydns.net ](https://whatsmydns.net/#CNAME).

### Hoe gebruik ik een opt-out-koppeling met CNAME

Als u CNAME gebruikt, zou de opt-out verbinding de &quot;client= `clientcode` parameter, bijvoorbeeld moeten bevatten:
`https://my.cname.domain/optout?client=clientcode` .

Vervang `clientcode` met uw cliëntcode, dan voeg de tekst of het beeld toe dat aan [ opt-out URL ](privacy/privacy.md) moet worden verbonden.

## Bekende beperkingen

* De modus QA blijft niet behouden wanneer u CNAME en at.js 1.x hebt, omdat deze is gebaseerd op een cookie van een andere fabrikant. Als tussenoplossing kunt u de voorvertoningsparameters toevoegen aan elke URL waarnaar u navigeert. De modus QA blijft behouden wanneer u CNAME en at.js 2.x hebt.
* Wanneer u CNAME gebruikt, neemt de kans toe dat de grootte van de cookieheader voor [!DNL Target] -aanroepen toeneemt. Adobe raadt aan de cookie kleiner te maken dan 8 kB.
