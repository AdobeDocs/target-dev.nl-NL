---
keywords: clientverzorging, naam, certificaatprogramma, canonieke naam, cookies, certificaat, amc, door adobe beheerd certificaat, digicert, domeinbesturingsvalidatie, dcv, clientverzorging2
description: Met [!UICONTROL Adobe Client Care] om CNAME (Canonical Name) steun in uit te voeren [!DNL Adobe Target] om ad-blocking kwesties te behandelen.
title: Hoe gebruik ik CNAME als doel?
feature: Privacy & Security
exl-id: 5709df5b-6c21-4fea-b413-ca2e4912d6cb
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 0%

---

# CNAME en Doel

Instructies voor het werken met [!DNL Adobe Client Care] om CNAME (Canonical Name) steun in uit te voeren [!DNL Adobe Target]. Gebruik CNAME om problemen met of beleid voor ITP-cookies (Intelligent Tracking Prevention) te verwerken en te blokkeren. Met CNAME, worden de vraag gemaakt aan een domein dat door de klant eerder dan een domein wordt bezeten van Adobe.

## Ondersteuning voor CNAME aanvragen in Doel

1. Bepaal de lijst met hostnamen die u nodig hebt voor uw SSL-certificaat (zie de Veelgestelde vragen hieronder).

1. Voor elke hostname, creeer een verslag van de NAAM in uw DNS richtend aan uw regelmatig [!DNL Target] hostnaam `clientcode.tt.omtrdc.net`.

   Als uw clientcode bijvoorbeeld &quot;naamloze gebruiker&quot; is en uw voorgestelde hostnaam `target.example.com`, ziet uw DNS CNAME-record er ongeveer als volgt uit:

   ```
   target.example.com.  IN  CNAME  cnamecustomer.tt.omtrdc.net.
   ```

   >[!WARNING]
   >
   >Adobe, DigiCert, kan pas een certificaat uitgeven als deze stap is voltooid. Daarom kan Adobe uw verzoek om een implementatie CNAME niet vervullen tot deze stap volledig is.

1. [Dit formulier invullen](assets/FPC_Request_Form.xlsx) en neemt het op wanneer u [een Adobe Client Care-ticket openen waarin CNAME-ondersteuning wordt aangevraagd](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?#reference_ACA3391A00EF467B87930A450050077C):

   * [!DNL Adobe Target] clientcode:
   * SSL-certificaathostnamen (voorbeeld: `target.example.com target.example.org`):
   * Aankoper van SSL-certificaat (Adobe wordt ten zeerste aanbevolen, zie Veelgestelde vragen): Adobe/klant
   * Als de klant het certificaat aanschaft, ook wel &#39;Create Your Own Certificate&#39; (BYOC) genoemd, voert u de volgende aanvullende gegevens in:
      * Certificaatorganisatie (bijvoorbeeld: Example Company Inc):
      * Organisatorische eenheid certificaat (optioneel, bijvoorbeeld: Marketing):
      * Certificaatland (voorbeeld: VS):
      * Certificaatstatus/regio (bijvoorbeeld: Californië):
      * Plaats van certificaat (voorbeeld: San Jose):

1. Als Adobe het certificaat aanschaft, werkt Adobe samen met DigiCert aan de aanschaf en implementatie van uw certificaat op Adobe productieservers.

   Als de klant het certificaat (BYOC) koopt, verzendt de Zorg van de Cliënt van Adobe u het certificaat ondertekenend verzoek (CSR). Gebruik de CSR wanneer u het certificaat aanschaft via de gekozen certificeringsinstantie. Nadat het certificaat wordt uitgegeven, verzend een exemplaar van het certificaat en om het even welke middencertificaten naar de Zorg van de Adobe Cliënt voor plaatsing.

   De Zorg van de Cliënt van Adobe brengt u op de hoogte wanneer uw implementatie klaar is.

1. Werk de `serverDomain` [documentatie](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverdomain) naar de nieuwe CNAME hostname en set `overrideMboxEdgeServer` tot `false` [documentatie](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#overridemboxedgeserver) in uw configuratie at.js.

## Veelgestelde vragen

De volgende informatie beantwoordt vaak gestelde vragen over het verzoeken van en het uitvoeren van de steun van CNAME in Doel:

### Kan ik mijn eigen certificaat opgeven (breng uw eigen certificaat of BYOC)?

U kunt uw eigen certificaat opgeven. Nochtans, adviseert Adobe deze praktijk niet. Het beheer van de SSL-certificaatlevenscyclus is zowel voor Adobe als voor u eenvoudiger als Adobe het certificaat koopt en beheert. SSL-certificaten moeten elk jaar worden vernieuwd. Daarom moet de Zorg van de Adobe Cliënt elk jaar met u contacteren om een nieuw certificaat te verkrijgen op een geschikte manier. Sommige klanten kunnen moeite hebben om een vernieuwd certificaat tijdig te produceren. Uw [!DNL Target] de implementatie wordt in gevaar gebracht wanneer het certificaat verloopt omdat browsers geen verbinding maken.

>[!WARNING]
>
>Als u een [!DNL Target] breng-uw-eigen implementatie van CNAME van het certificaat, bent u verantwoordelijk voor het verstrekken van vernieuwde certificaten aan de Zorg van de Adobe Cliënt elk jaar. Het toestaan van uw certificaat van de NAAM om te verlopen alvorens Adobe een vernieuwd certificaat kan opstellen resulteert in een stroomonderbreking voor uw specifiek [!DNL Target] uitvoering.

### Hoe lang tot mijn nieuwe SSL certificaat verloopt?

Alle Adobe-gekochte certificaten zijn één jaar geldig. Zie [Het artikel van DigiCert over 1 jaar certificaten](https://www.digicert.com/blog/position-on-1-year-certificates) voor meer informatie .

### Welke hostnames moet ik kiezen? Hoeveel hostnames per domein zou ik moeten kiezen?

De implementaties van CNAME van het doel vereisen slechts één hostname per domein op het SSL certificaat en in DNS van de klant. Adobe raadt één hostnaam per domein aan. Sommige klanten vereisen meer hostnames per domein voor hun eigen doeleinden (bijvoorbeeld het testen in het opvoeren), wat wordt ondersteund.

De meeste klanten kiezen een hostnaam als `target.example.com`. Adobe beveelt aan deze praktijk te volgen, maar uiteindelijk is de keuze aan u. Vraag geen hostname van een bestaand DNS verslag aan. Dit veroorzaakt een conflict en vertraagt de tijd om uw [!DNL Target] CNAME request.

### Ik heb al een CNAME-implementatie voor Adobe Analytics. Kan ik hetzelfde certificaat of dezelfde hostnaam gebruiken?

Nee, [!DNL Target] vereist een aparte hostnaam en certificaat.

### Is mijn huidige implementatie van [!DNL Target] beïnvloed door ITP 2.x?

Apple Intelligent Tracking Prevention (ITP) versie 2.3 introduceerde de CNAME Camaking Mitigation-functie, die kan detecteren [!DNL Target] De implementaties van CNAME en vermindert het verlopen van het koekje tot zeven dagen. Momenteel [!DNL Target] heeft geen oplossing voor de Beperking van de Camouflatie van de NAAM van ITP. Voor meer informatie over ITP, zie [Apple Intelligent Tracking Prevention (ITP) 2.x](../before-implement/privacy/apple-itp-2x.md).

### Welk soort de dienstverstoringen kan ik verwachten wanneer mijn implementatie CNAME wordt opgesteld?

Er is geen de dienstverstoring wanneer het certificaat wordt opgesteld (met inbegrip van certificaatvernieuwingen).

Nochtans, nadat u hostname in uw [!DNL Target] uitvoeringscode (`serverDomain` in at.js) aan nieuwe CNAME hostname (`target.example.com`), worden terugkerende bezoekers door webbrowsers behandeld als nieuwe bezoekers. Het retourneren van de profielgegevens van bezoekers gaat verloren omdat het vorige cookie niet toegankelijk is onder de oude hostnaam (`clientcode.tt.omtrdc.net`). De vorige cookie is niet toegankelijk vanwege beveiligingsmodellen van de browser. Deze verstoring komt slechts op de aanvankelijke besnoeiing-over aan nieuwe CNAME voor. Certificaatverlengingen hebben niet hetzelfde effect omdat de hostnaam niet verandert.

### Welk zeer belangrijk type en algoritme van de certificaathandtekening voor mijn implementatie CNAME wordt gebruikt?

Alle certificaten zijn RSA SHA-256 en de sleutels zijn RSA 2048 beetje, door gebrek. Toetsgrootten die groter zijn dan 2048 bits, worden momenteel niet ondersteund.

### Hoe kan ik bevestigen dat mijn implementatie CNAME klaar voor verkeer is?

Gebruik de volgende set opdrachten (in de opdrachtregelterminal van macOS of Linux, met bash en curl >=7.49):

1. Kopieer en plak deze basfunctie in uw terminal, of plak de functie in uw basale startmanuscriptdossier (gewoonlijk `~/.bash_profile` of `~/.bashrc`) zodat de functie beschikbaar is over eindzittingen:

   ```
   function adobeTargetCnameValidation {
     local hostname="$1"
     if [ -z "$hostname" ]; then
       echo "ERROR: no hostname specified"
       return 1
     fi
   
     local service="Adobe Target CNAME implementation"
     local edges="31 32 34 35 36 37 38"
     local edgeDomain="tt.omtrdc.net"
     local edgeFormat="mboxedge%d%s.$edgeDomain"
     local shardFormat="-alb%02d"
     local shards=5
     local shardsFoundCount=0
     local shardsFound
     local shardsFoundOutput
     local curlRegex="subject:.*CN=|expire date:|issuer:"
     local curlValidation="SSL certificate verify ok"
     local curlResponseValidation='"OK"'
     local curlEndpoint="/uptime?mboxClient=uptime3"
     local url="https://$hostname$curlEndpoint"
     local sslLabsUrl="https://ssllabs.com/ssltest/analyze.html?hideResults=on&latest&d=$hostname"
     local success="✅"
     local failure="🚫"
     local info="🔎"
     local rule="="
     local horizontalRule="$(seq ${COLUMNS:-30} | xargs printf "$rule%.0s")"
     local miniRule="$(seq 5 | xargs printf "$rule%.0s")"
     local curlVersion="$(curl --version | head -1 | cut -d' ' -f2 )"
     local curlVersionRequired=">=7.49"
     local edgeCount="$(wc -w <<< "$edges" | tr -d ' ')"
     local edge
     local shard
     local currEdgeShard
     local dnsOutput
     local cnameExists
     local endToEndTestSucceeded
     local curlResult
   
     for shard in $(seq $shards); do
       if [ "$shardsFoundCount" -eq 0 ]; then
         for edge in $edges; do
           if [ "$shard" -eq 1 ]; then
             currEdgeShard="$(printf "$edgeFormat" "$edge" "")"
           else
             currEdgeShard="$(
               printf "$edgeFormat" "$edge" "$(
                 printf -- "$shardFormat" "$shard"
               )"
             )"
           fi
           curlResult="$(curl -vsm20 --connect-to "$hostname:443:$currEdgeShard:443" "$url" 2>&1)"
           if grep -q "$curlValidation" <<< "$curlResult"; then
             shardsFound+=" $currEdgeShard"
             if grep -q "$curlResponseValidation" <<< "$curlResult"; then
               shardsFoundCount=$((shardsFoundCount+1))
               shardsFoundOutput+="\n\n$miniRule $success $hostname [edge shard: $currEdgeShard] $miniRule\n"
             else
               shardsFoundOutput+="\n\n$miniRule $failure $hostname [edge shard: $currEdgeShard] $miniRule\n"
             fi
             shardsFoundOutput+="$(grep -E "$curlRegex" <<< "$curlResult" | sort)"
             if ! grep -q "$curlResponseValidation" <<< "$curlResult"; then
               shardsFoundOutput+="\nERROR: unexpected HTTP response from this shard using $url"
             fi
           fi
         done
       fi
     done
   
     echo
     echo "$horizontalRule"
     echo
     echo "$service validation for hostname $hostname:"
     dnsOutput="$(dig -t CNAME +short "$hostname" 2>&1)"
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
   
     curlResult="$(curl -vsm20 "$url" 2>&1)"
     if grep -q "$curlValidation" <<< "$curlResult"; then
       if grep -q "$curlResponseValidation" <<< "$curlResult"; then
         echo -en "$success $hostname passes TLS and HTTP response validation"
         if [ -n "$cnameExists" ]; then
           echo
         else
           echo " -- the DNS CNAME is not pointing to the correct subdomain for ${service}s with Adobe-managed certificates" \
             "(bring-your-own-certificate implementations don't have this requirement), but this test passes as configured"
         fi
         endToEndTestSucceeded=true
       else
         echo -n "$failure $hostname FAILED HTTP response validation --" \
           "unexpected response from $url -- "
         if [ -n "$cnameExists" ]; then
           echo "DNS is NOT pointing to the correct shard, notify Adobe Client Care"
         else
           echo "the required DNS CNAME record is missing, see above"
         fi
       fi
     else
   
       echo -n "$failure $hostname FAILED TLS validation -- "
       if [ -n "$cnameExists" ]; then
         echo "DNS is likely NOT pointing to the correct shard or there's a validation issue with the certificate or" \
           "protocols, see curl output below and optionally SSL Labs ($sslLabsUrl):"
         echo ""
         echo "$horizontalRule"
         echo "$curlResult" | sed 's/^/    /g'
         echo "$horizontalRule"
         echo ""
       else
         echo "the required DNS CNAME record is missing, see above"
       fi
     fi
   
     if [ "$shardsFoundCount" -ge "$edgeCount" ]; then
       echo -n "$success $hostname passes shard validation for the following $shardsFoundCount edge shards:"
       echo -e "$shardsFoundOutput"
       echo
   
       if [ -n "$cnameExists" ] && [ -n "$endToEndTestSucceeded" ]; then
         echo "$horizontalRule"
         echo ""
         echo "  For additional TLS/SSL validation, including detailed browser/client support,"
         echo "  see SSL Labs (click the first IP address if prompted):"
         echo ""
         echo "    $info  $sslLabsUrl"
         echo ""
         echo "  To check DNS propagation around the world, see whatsmydns.net:"
         echo ""
         echo "    $info  DNS A records:     https://whatsmydns.net/#A/$hostname"
         echo "    $info  DNS CNAME record:  https://whatsmydns.net/#CNAME/$hostname"
       fi
     else
       echo -n "$failure $hostname FAILED shard validation -- shards found: $shardsFoundCount," \
         "expected: $edgeCount"
       if bc -l <<< "$(cut -d. -f1,2 <<< "$curlVersion") $curlVersionRequired" 2>/dev/null | grep -q 0; then
         echo -n " -- insufficient curl version installed: $curlVersion, but this script requires curl version" \
           "$curlVersionRequired because it uses the curl --connect-to flag to bypass DNS and directly test" \
           "each Adobe Target edge shards' SNI confirguation for $hostname"
       fi
       if [ -n "$shardsFoundOutput" ]; then
         echo -e ":\n$shardsFoundOutput"
       fi
       echo
     fi
     echo
     echo "$horizontalRule"
     echo
   }
   ```

1. Deze opdracht plakken (vervangen `target.example.com` met uw hostnaam):

   ```
   adobeTargetCnameValidation target.example.com
   ```

   Als de implementatie gereed is, ziet u de uitvoer hieronder. Het belangrijkste onderdeel is dat alle validatiestatus regels toont `✅` eerder dan `🚫`. Elke CNAME-schaduw van de doelrand moet worden weergegeven `CN=target.example.com`, die overeenkomt met de primaire hostnaam op het aangevraagde certificaat (extra SAN-hostnamen op het certificaat worden niet afgedrukt in deze uitvoer).

   ```
   $ adobeTargetCnameValidation target.example.com
   
   ==========================================================
   
   Adobe Target CNAME implementation validation for hostname target.example.com:
   ✅ target.example.com passes DNS CNAME validation
   ✅ target.example.com passes TLS and HTTP response validation
   ✅ target.example.com passes shard validation for the following 7 edge shards:
   
   ===== ✅ target.example.com [edge shard: mboxedge31-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge32-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge34-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge35-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge36-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge37-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge38-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ==========================================================
   
     For additional TLS/SSL validation, including detailed browser/client support,
     see SSL Labs (click the first IP address if prompted):
   
       🔎  https://ssllabs.com/ssltest/analyze.html?hideResults=on&latest&d=target.example.com
   
     To check DNS propagation around the world, see whatsmydns.net:
   
       🔎  DNS A records:     https://whatsmydns.net/#A/target.example.com
       🔎  DNS CNAME record:  https://whatsmydns.net/#CNAME/target.example.com
   
   ==========================================================
   ```

>[!NOTE]
>
>Als dit bevestigingsbevel op DNS bevestiging ontbreekt maar u reeds de noodzakelijke DNS veranderingen hebt aangebracht, zou u op uw DNS updates kunnen moeten wachten om volledig te verspreiden. DNS-records hebben een koppeling [TTL (time-to-live)](https://en.wikipedia.org/wiki/Time_to_live#DNS_records) die de tijd van de geheim voorgeheugenvervaldatum voor DNS antwoorden van die verslagen dicteert. Dientengevolge, zou u minstens zolang uw TTLs kunnen moeten wachten. U kunt de `dig target.example.com` of [De G Suite Toolbox](https://toolbox.googleapps.com/apps/dig/#CNAME) om uw specifieke TTLs op te zoeken. Om DNS propagatie rond de wereld te controleren, zie [whatsmydns.net](https://whatsmydns.net/#CNAME).

### Hoe gebruik ik een opt-out-koppeling met CNAME

Als u CNAME gebruikt, zou de opt-out verbinding &quot;client= moeten bevatten`clientcode` parameter, bijvoorbeeld:
`https://my.cname.domain/optout?client=clientcode`.

Vervangen `clientcode` met uw clientcode, voegt u vervolgens de tekst of afbeelding toe die u wilt koppelen aan de [opt-out-URL](privacy/privacy.md).

## Bekende beperkingen

* De modus QA blijft niet behouden wanneer u CNAME en at.js 1.x hebt, omdat deze is gebaseerd op een cookie van een andere fabrikant. Als tussenoplossing kunt u de voorvertoningsparameters toevoegen aan elke URL waarnaar u navigeert. De modus QA blijft behouden wanneer u CNAME en at.js 2.x hebt.
* Als u CNAME gebruikt, is het waarschijnlijker dat de grootte van de cookieheader voor [!DNL Target] de vraagverhoging. Adobe raadt aan de cookie kleiner te maken dan 8 kB.
