---
description: 'null'
seo-description: 'null'
seo-title: Kommandoradsanvändning för principhanteraren
title: Kommandoradsanvändning för principhanteraren
uuid: 9b17bc9a-0b1b-405f-a62b-0310c43c9255
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---


# Kommandoradsanvändning för principhanteraren {#policy-manager-command-line-usage}

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

**Tabell 1: Kommandon**

| Kommando | Beskrivning |
|---|---|
| `new` | Skapar en ny DRM-princip |
| `detail` | Beskriver en befintlig DRM-princip |
| `update` | Uppdaterar en befintlig DRM-princip |

**Tabell 2: Alternativ**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Kommandoradsalternativ </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Beskrivning </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c configfile  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger namn och plats för konfigurationsfilen. </p> <p class="- topic/p ">Om du inte anger ett namn eller en plats söker DRM Policy Manager efter <span class="filepath"> flashaccesstools.properties </span> i den aktuella arbetskatalogen. </p> <p>Obs!  De alternativ som du anger på kommandoraden åsidosätter de alternativ som du anger i konfigurationsfilen. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Om målfilen finns kan du skriva över den utan att uppmanas till det. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Fråga inte om målfilen ska skrivas över. Om målfilen finns och <span class="codeph"> -o </span> inte har angetts inträffar ett fel. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger att DRM-principen har en rotlicens. </p> <p class="- topic/p ">Det här alternativet är inte tillgängligt för uppdateringar. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e datum  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Datumet innan licenserna börjar gälla. </p> <p>Du kan ange datumet i formatet <span class="+ topic/ph pr-d/codeph codeph"> ååå-mm-dd </span> eller <span class="+ topic/ph pr-d/codeph codeph"> ååå-mm-dd-h24:min:sek </span>. Exempel: 2008-12-1 eller 2008-12-1-00:00:00 för midnatt den 1 december 2008. </p> <p> 
     <ul id="ul_D5DB5044756D4BD6A734813971598425"> 
      <li id="li_B6BD62A524384060A9DDA14FF50936FA">Värdet måste vara större än värdet för <span class="codeph"> -s </span> om det finns. </li> 
      <li id="li_C3C5AD0231A240EC9AC57685B9206E8D">Du kan inte använda det här alternativet med <span class="codeph"> -r </span>. </li> 
      <li id="li_3790E2F829A149979BF44E0914CFF431">Om du vill ta bort slutdatumet när du uppdaterar en DRM-princip ska du använda <span class="codeph"> -e </span> utan att ange ett datum. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r minuter  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Den varaktighet i minuter som det skyddade innehållet är giltigt. </p> <p class="- topic/p ">DRM-principen blir giltig när innehållet skyddas med paketeraren. </p> <p> 
     <ul id="ul_4690A0E4677A4DF6A006B7FCBD46F1BE"> 
      <li id="li_D1F098D44B494EE7A8647C0B62D5ACFA">Värdet får inte vara negativt. </li> 
      <li id="li_ADFDCB01EEE04B37AFA42886AAEF47EB">Du kan inte använda det här alternativet tillsammans med <span class="codeph"> -e </span>. </li> 
      <li id="li_E80563E68BEB43FC9E29A694594CAE01">Om du vill ta bort eller ta bort varaktigheten när du uppdaterar en DRM-princip ska du använda <span class="codeph"> -r </span> utan att ange några minuter. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s datum  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Det datum då licenserna blir giltiga. </p> <p>Du kan ange datumet i formatet <span class="+ topic/ph pr-d/codeph codeph"> ååå-mm-dd </span> eller <span class="+ topic/ph pr-d/codeph codeph"> ååå-mm-dd-h24:min:sek </span>. Exempel: <span class="codeph"> 2008-12-1 </span> eller <span class="codeph"> 2008-12-1-00:00:00 </span> för midnatt 1 december 2008. </p> <p> 
     <ul id="ul_D52B337F547F4E7AB87FE025236CA930"> 
      <li id="li_DBAE380972434DB1A4EF20D399038AB8">Värdet måste vara mindre än värdet för <span class="codeph"> -e </span>, om det finns. </li> 
      <li id="li_2899EC5559CF44319A4AC4ECD90A5B9A">Du kan inte använda det här alternativet tillsammans med <span class="codeph"> -r </span>. </li> 
      <li id="li_19861B1A64E44B95B649948EAB3E4085">Om du vill ta bort eller ta bort startdatumet när du uppdaterar en DRM-princip använder du <span class="codeph"> -s </span> utan att ange ett datum. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w [&lt;minutes&gt;[,enableHS|disableHS]]  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Uppspelningsfönstret, vilket är antalet minuter som innehållet kan visas från den första uppspelningen. </p> <p>Om det är ospecificerat, eller om <span class="codeph"> -w </span> används utan att ett antal minuter anges, finns det ingen begränsning för uppspelningsfönstret. Värdet får inte vara negativt. </p> <p>Valfri <span class="codeph"> enableHS </span> eller <span class="codeph"> disableHS </span>-flagga signalerar om stopp ska aktiveras eller inaktiveras. Flaggan anger om dekrypteringskontexten förstörs i slutet av uppspelningsfönstret (aktiverat) eller inte förstörs (inaktiverat). </p> <p>Om du till exempel vill ange att innehållet bara får visas i 60 minuter och kräver ett stopp: 
     <codeblock>
       -w&amp;nbsp;60,enableHS 
     </codeblock> </p> <p>Obs!  <i>Hård stopp</i> stöds för närvarande inte i Flash Player, Android och iOS. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l minuter  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Licensens cachelagringstid är den tid i minuter som en licens kan cachas i klientens License Store efter att licensen har utfärdats av servern. Värdet får inte vara negativt. </p> <p>Du kan ange <span class="codeph"> -l 0 </span> för att ange att licenscache-lagring inte är tillåten. För obegränsad licenscachelagring anger du <span class="codeph"> -l </span> utan några minuter. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Licensens slutdatum för cachelagring. </p> <p class="- topic/p ">Detta anger det sista datumet då klienten kan cachelagra licenser i klientens licensarkiv efter att Primetime DRM-servern har utfärdat licensen. </p> <p>Du kan ange datumet i följande format: 
     <ul id="ul_112DE7248A9C48B19520A3AA9E5D1F03"> 
      <li id="li_01C5400E78B84A3B8955972FBA875AAC"> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd  </span> </li> 
      <li id="li_AA13B1EFA07A4542A3DB41FA3320B143"> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sek  </span> </li> 
     </ul>Exempel: <span class="codeph"> 2008-12-1 </span> eller <span class="codeph"> 2008-12-1-00:00:00 </span> för midnatt 1 december 2008. Du måste använda <span class="codeph"> -l </span> utan att ange några minuter för obegränsad licenscachelagring. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Namnområdet för autentisering. </p> <p class="- topic/p ">Om du använder det här alternativet måste klienten ange ett användarnamn och lösenord som utfärdades av den angivna utfärdaren. </p> <p>Du kan inte använda det här alternativet tillsammans med <span class="codeph"> -x </span>. </p> <p>Det här alternativet är inte tillåtet för uppdateringar. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Tillåt anonym åtkomst. </p> <p class="- topic/p ">Du kan inte använda det här alternativet tillsammans med <span class="codeph"> -authNS </span>. </p> <p class="- topic/p ">Det här alternativet är inte tillåtet för uppdateringar. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId  </span>[:  <span class="+ topic/ph pr-d/codeph codeph"> appId  </span>[:[  <span class="+ topic/ph pr-d/codeph codeph"> min  </span>]:[  <span class="+ topic/ph pr-d/codeph codeph"> max  </span>]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">En tillåtelselista med AIR-program som kan spela upp skyddat innehåll. </p> <p class="- topic/p ">Du kan använda det här alternativet om du vill begränsa vilka utgivare, program och versioner som kan få åtkomst till innehåll som är skyddat med den här DRM-principen. </p> <p class="- topic/p ">Om du inte anger <i class="+ topic/ph hi-d/i ">appId</i> tillåts alla program för utgivaren <i class="+ topic/ph hi-d/i ">pubId</i>. </p> <p>Obs!  <i class="+ topic/ph hi-d/i ">min</i> och <i class="+ topic/ph hi-d/i ">max</i> versionsnummer är valfria. </p> <p class="- topic/p ">Du kan ange flera <span class="codeph"> -air </span>-alternativ för att tillåta flera program. Om du inte anger något AIR- eller SWF-program kan alla program få åtkomst till det här innehållet. Om du vill ta bort eller ta bort alla poster från listan under en uppdatering använder du <span class="codeph"> -air </span> utan de återstående argumenten. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist name  </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> value  </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> pairs  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM-klienterna som är begränsade från åtkomst till skyddat innehåll. </p> <p class="- topic/p ">Värdet stöder kommaavgränsade namn:värdepar i följande format: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | release= stringValue  </span> </p> <p class="- topic/p ">Exempel: <span class="codeph"> os=Win,release=2.0.1 </span>. Om du under en uppdatering vill ta bort alla poster från listan använder du <span class="codeph"> -drmBlacklist </span> utan de återstående argumenten. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger att DRM-klienter måste ha en tilldelad lägsta säkerhetsnivå för att få åtkomst till skyddat innehåll. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE | KRÄVS | NO_PLAYBACK | REQUIRED_ACP | REQUIRED_CGMSA | USE_IF_AVAILABLE_ACP | USE_IF_AVAILABLE_CGMSA  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Begränsningar för analogt utdataskydd </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | KRÄVS | NO_PLAYBACK  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Begränsningar för skydd av digitala utdata </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist name  </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> value  </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> pairs  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">De programkörningsmiljöer som är begränsade från åtkomst till skyddat innehåll. </p> <p class="- topic/p ">Värdet stöder kommaavgränsat namn:värdepar i följande format: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | program | release= stringValue  </span> </p> <p class="- topic/p ">Exempel: <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. Om du under en uppdatering vill ta bort alla poster från listan använder du <span class="codeph"> -runtimeBlacklist </span> utan de återstående argumenten. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger att programkörningsversionerna måste ha en angiven lägsta säkerhetsnivå för att kunna komma åt skyddat innehåll. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url  </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf file= swf_file  </span>,  <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">En tillåtelselista med SWF-program som kan spela upp skyddat innehåll. </p> <p class="- topic/p ">Du kan ange flera <span class="codeph"> -swf </span>-alternativ för att tillåta flera program. Om du inte anger något AIR- eller SWF-program kan alla program få åtkomst till det här innehållet. </p> <p>Om du vill ta bort alla poster från listan under en uppdatering använder du <span class="codeph"> -swf </span> utan de återstående argumenten. Om du vill identifiera en SWF-fil med dess hash-värde måste du ange för vilken SWF-fil hash ska beräknas och den maximala tiden som SWF-verifieringen ska slutföras (i sekunder). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= värde  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger anpassade nycklar/värden som du vill lägga till i en DRM-princip. </p> <p class="- topic/p ">Du kan ange flera <span class="codeph"> -k </span>-alternativ. Under uppdateringen kan du använda <span class="codeph"> -k </span> utan de återstående argumenten om du vill ta bort alla egenskaper. Tolkningen eller hanteringen av data hanteras av DRM-licensservern Primetime. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name= value  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Lägger till en anpassad egenskap som visas i licensen som genereras för varje klient. </p> <p class="- topic/p ">Du kan ange flera alternativ för <span class="codeph"> -p </span> om du vill lägga till flera egenskaper. Under en uppdatering måste du använda <span class="codeph"> -p </span> utan de återstående argumenten om du vill ta bort alla egenskaper. Tolkningen eller hanteringen av dessa data hanteras av implementeringen av klientprogrammet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> <span class="codeph"> -opOTA whitelist=&lt;connection types=""&gt; </span> </span> </td> 
   <td colname="2" class="- topic/entry "> OTA-begränsningar (over the air) för skydd av utdata. Fältet <span class="codeph"> whitelist </span> anger vilka anslutningstyper som ska användas i tillåtelselista och formatet &lt;anslutningstyper&gt; är <span class="codeph"> [type(,typ)*] </span>, där typen kan vara något av följande: MIRACAST, AIRPLAY, WIDI, DLNA </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opResolution  &lt;filename&gt; </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Upplösningsbaserade begränsningar för utdataskydd som definieras i den angivna filen. </p> <p>Kodningen för den här filen är JSON. Grammatiken för formateringen finns i <i>Om upplösningsbaserat utdataskydd</i>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Exempel**

Så här skapar du en profil som tillåter anonym åtkomst till ditt innehåll med hjälp av din egen konfigurationsegenskapsfil:

```
java -jar libs\AdobePolicyManager.jar new policy_test.pol -x -c my_configuration.properties
```
