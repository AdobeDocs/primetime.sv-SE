---
title: Egenskaper för konfigurationsfil
description: Egenskaper för konfigurationsfil
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---

# Egenskaper för konfigurationsfil {#configuration-file-properties}

Konfigurationsfilen anger följande egenskaper. För egenskapsnamn som innehåller `n`, `n` representerar ett heltal som börjar med 1 och ökar för varje instans av egenskapen.

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Alternativ för egenskap/kommandorad </th> 
   <th colname="2" class="- topic/entry entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -n</span> <i class="+ topic/ph hi-d/i ">principnamn</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Principnamnet som kan läsas av människor. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> <i class="+ topic/ph hi-d/i ">boolesk</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Om värdet är true krävs en HTTPS Key Server för nyckelleverans till iOS. Standardvärdet är false om det inte anges. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.enforcementJailbreak</span> <p class="- topic/p "><span class="codeph"> -enforcementJailbreak</span> <i class="+ topic/ph hi-d/i ">boolesk</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Om värdet är true tillåts inte uppspelning på enheter som stöder jailbreak-identifiering om jailbreak har upptäckts. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -kritisk</span> <i class="+ topic/ph hi-d/i ">boolesk</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Ställ in kritisk policy. Om värdet är true måste servern förstå alla delar av principen (det här är standardbeteendet). Om värdet är false kan servern ignorera principattribut som den inte förstår. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">Licensservercertifikat vars offentliga nyckel används för att kryptera rotkrypteringsnyckeln för <a href="../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md" format="dita" scope="local"> Förbättrad licenskedja </a>
   This property specifies a file that contains the certificate only (either PEM or DER format is acceptable). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">rotnyckel</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Ange rotkrypteringsnyckeln för den förbättrade licenskopplingen. Om ingen nyckel har angetts och Förbättrad licenskoppling är aktiverad, genereras en slumpmässig nyckel. Nyckeln måste vara 16 byte lång och anges som hex-värden. Det är valfritt att använda mellanrum mellan hexadecimala värden. För uppdateringar tillåts inte kommandoradsalternativet och egenskapen ignoreras. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -domainURL</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry "> URL för domänservern, om domänregistrering krävs. För uppdateringar tillåts inte kommandoradsalternativet och egenskapen ignoreras. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry "> Anger om anonym domänregistrering tillåts. Ange egenskapen till true eller inkludera det här kommandoradsalternativet för att tillåta anonym åtkomst. Det här alternativet kan inte användas med -domainAuthNS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> <i class="+ topic/ph hi-d/i ">namespace</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Autentiseringsnamnområdet för domänregistrering. Om det anges bör klienten autentisera med ett användarnamn och lösenord som utfärdats av den angivna utfärdaren. För uppdateringar tillåts inte kommandoradsalternativet och egenskapen ignoreras. Det här alternativet kan inte användas med -domainAnon. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -opAnalog</span> <i class="+ topic/ph hi-d/i ">AnalogOption</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Begränsningar för analogt utdataskydd. Följande värden stöds: 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_5BC8F39B61894E83A7B27570FF848F09"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PROTECTION</span> </p> </li> 
     <li class="- topic/li " id="li_FF14594A0714480496793A82C3FA1610"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </p> </li> 
     <li class="- topic/li " id="li_721FCC4DC1F34AE398EFAE4C0D3F50F5"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_D588BB278BEE4CEAB034BD48550EBCDC"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_7E5F006D2F114502BA6D0A9C4173004E"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> KRÄVS</span> </p> </li> 
     <li class="- topic/li " id="li_9EBFAA4AACF249C2A94432D88E12C3B9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_6720C6A085864BEB957C0BF2C38551C9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_6FD98473ECDB4A66AC4B506FB9B3B360"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -drmBlacklist</span> <i class="+ topic/ph hi-d/i ">namn/värde-par</i> </p> </td> 
   <td colname="2" class="- topic/entry ">DRM-klienter hindrade från att komma åt skyddat innehåll. Det här alternativet anger en lista med versioner av DRM-moduler som inte får användas (blockeringslista). Värdet består av kommaavgränsade namn=värde-par med följande format: <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Ytterligare namn/värde-par måste vara kommaavgränsade. Till exempel: <span class="codeph"> os=Win,release=2.0,arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklsit</span> <i class="+ topic/ph hi-d/i ">namn/värde-par</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Programkörningsmiljöerna hindrade från att komma åt skyddat innehåll. Det här alternativet anger en lista med versioner av runtime-moduler som inte får användas (blockeringslista). Värdet består av kommaavgränsade namn=värde-par med följande format: <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|program|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Ytterligare namn/värde-par måste vara kommaavgränsade. Till exempel: <span class="codeph"> os=Win,application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">namn/värde-par</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger vilka enhetsfunktioner som krävs för att få åtkomst till skyddat innehåll. Värdet består av kommaavgränsade namn=värde-par med följande format: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">Till exempel: <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>. Använd <span class="codeph"> -devCapabilitiesV1</span> utan de återstående argumenten för att ta bort begränsningen av enhetsfunktioner. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -sync</span> <i class="+ topic/ph hi-d/i ">namn/värde-par</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Ange hur ofta klienter måste skicka synkroniseringsmeddelanden till servern. Om den inte anges skickar klienterna inte synkroniseringsmeddelanden när innehåll som är skyddat med den här principen spelas upp. Värdet består av kommaavgränsade <span class="codeph"> name=value</span> par med följande format: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force|hardStop=numberValue</span> </p> <p class="- topic/p "> 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_25CAF96C27F34848A95B2E3693847C71"><span class="codeph"> start</span> (obligatoriskt) - Startintervall anger att klienten ska starta synkroniseringen med servern så här många minuter sedan den senaste synkroniseringen. </li> 
      <li id="li_CC9068CFE75645029C947C9E1B53351F"><span class="codeph"> force</span> (valfritt) - Sannolikheten för framtvingad synkronisering är den sannolikhet (0-100) med vilken klienten ska framtvinga ett synkroniseringsmeddelande under uppspelning. </li> 
      <li id="li_C31A6250F19348FBB8B7569D00C6314E"><span class="codeph"> hardStop</span> (valfritt) - Hårt stoppintervall är den tid i minuter efter vilken klienten kommer att misslyckas med uppspelningen om det inte går att synkronisera. Om den anges måste den vara större än startintervallet. </li> 
     </ul>Använd <span class="codeph"> -sync</span> utan de återstående argumenten för att ta bort synkroniseringskraven. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">Anger om den här principen har en rotlicens (se <i class="+ topic/ph hi-d/i ">Förbättrad licenskedja</i> in <i class="+ topic/ph hi-d/i ">Använda Adobe Access för att skydda innehåll</i>). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">Det datum efter vilket innehållet är giltigt. Använd formatet <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> (till exempel <span class="codeph"> 2009-01-31</span> representerar 31 januari kl. 12.00) eller <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sek</span> (till exempel <span class="codeph"> 2009-01-31-14:30:00</span> representerar 31 januari klockan 2:30). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Det datum före vilket innehållet är giltigt. Båda <span class="codeph"> policy.expiration.endDate</span> och policy.expiration.duration får inte anges samtidigt. Använd formatet <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> eller <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sek</span> (till exempel 2009-01-31-14:30:00 representerar 31 januari klockan 2:30). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Den tid som innehållet är giltigt (i minuter), med början när det paketeras. Båda <span class="codeph"> policy.expiration.endDate</span> och <span class="codeph"> policy.expiration.duration</span> får inte anges samtidigt. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Den tid en licens kan cachas på klienten (i minuter). Ange den här egenskapen till 0 om du inte vill tillåta licenscachelagring. Värdet måste vara 0 eller högre. Båda <span class="codeph"> policy.licenseCaching.duration</span> och <span class="codeph"> policy.licenseCaching.endDate</span> Ska inte användas samtidigt. </p> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Anteckning</b>: Den här principinställningen används endast för licenscachning på disken. Det styr inte längden på den cachelagrade licensen för minnet. Licensen kan cachelagras på minnet även om den angivna varaktigheten är noll. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Datumet efter vilket licenser inte får cachas. Båda <span class="codeph"> policy.licenseCaching.duration</span> och <span class="codeph"> policy.licenseCaching.endDate</span> Ska inte användas samtidigt. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger om anonym licensköp tillåts. Standardvärdet är "false" (autentisering av användarnamn/lösenord krävs) om det inte anges. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Om autentisering av användarnamn/lösenord krävs anger den här egenskapen en valfri namnkvalificerare för användarnamn. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anpassade namn/värde-par som ska användas av servern vid licensköp. Använd följande format för att ange egenskaper: <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger uppspelningsfönstret (i minuter), vilket är den tid som licensen gäller för efter första gången som den används för att spela upp skyddat innehåll. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Begränsningar för utdataskydd. Värdena måste vara något av följande: </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">NO_PROTECTION, USE_IF_AVAILABLE, REQUIRED, NO_PLAYBACK</i> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM-modulen måste ha den angivna lägsta säkerhetsnivån, eller högre, för att kunna komma åt skyddat innehåll. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Programmets körningsmodul måste ha den angivna lägsta säkerhetsnivån, eller högre, för att kunna komma åt skyddat innehåll. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">En tillåtelselista av Adobe AIR- eller iOS-programmen tillåter uppspelning av skyddat innehåll. Egenskapen måste ha följande format: <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">En tillåtelselista av programmen i SWF kunde spela upp skyddat innehåll. Använd följande format: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">URL</span> eller file=<span class="+ topic/ph pr-d/codeph codeph">swf_file</span>,time=<i class="+ topic/ph hi-d/i ">max_time_to_verify</i> <i class="+ topic/ph hi-d/i ">swf_file</i> är SWF-filen som hashen ska beräknas för, och <i class="+ topic/ph hi-d/i ">max_time_to_verify</i> är den längsta tid som SWF kan ladda ned och bekräfta (i sekunder). </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anpassade namn/värde-par som ska inkluderas i licenser som utfärdas till användare. Använd följande format: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> <p class="- topic/p ">Det här alternativet kan definieras flera gånger för flera anpassade egenskaper. </p> </td> 
  </tr> 
 </tbody> 
</table>
