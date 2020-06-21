---
seo-title: Användning av kommandorad
title: Användning av kommandorad
uuid: e549a98e-b027-4472-8860-6aa1d56d4a8b
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---


# Användning av kommandorad {#command-line-usage}

Innan du använder Policy Manager måste du se till att du uppfyller de krav som listas i Krav.

Policy Manager finns i [!DNL \Reference Implementation\Command Line Tools] katalogen på dvd-skivan. Använd följande syntax när du kör verktyget:

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

Följande tabell innehåller beskrivningar av kommandoradsåtgärderna som visas i syntaxen ovan:

| Kommandoradsåtgärd | Beskrivning |
|---|---|
| `new` | Skapar en ny princip. |
| `detail` | Beskriver en befintlig princip. |
| `update` | Uppdaterar en befintlig princip. |

I följande tabell beskrivs de kommandoradsalternativ som kan anges tillsammans med syntaxen ovan:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Kommandoradsalternativ </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Beskrivning </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c configfile </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger platsen för konfigurationsfilen. Om det här alternativet inte används söker principhanteraren efter <span class="filepath"> flashaccesstools.properties </span> i arbetskatalogen. De alternativ som anges på kommandoraden har företräde framför de som finns i konfigurationsfilen. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Om målfilen redan finns skriver du över den utan att fråga. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Fråga inte om målfilen ska skrivas över. Om målfilen redan finns och <span class="codeph"> -o inte </span> är inställd returneras ett fel. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger att principen har en rotlicens. Tillåts inte för uppdateringar. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e datum </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Det datum som licenserna ska gälla före. Ange som <span class="+ topic/ph pr-d/codeph codeph"> åååå-mm-dd </span> eller <span class="+ topic/ph pr-d/codeph codeph"> åååå-mm-dd-h24:min:sek </span>. Exempel: 2008-12-1 eller 2008-12-1-00:00:00 för midnatt den 1 december 2008. Värdet måste vara större än värdet för <span class="codeph"> -s </span>om det finns. Det här alternativet kan inte användas med <span class="codeph"> -r </span>. Om du vill ta bort slutdatumet när du uppdaterar en princip använder du <span class="codeph"> -e </span> utan att ange ett datum. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r minuter </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Den varaktighet (minuter) som innehåll som skyddas med den här principen är giltig, med början när innehållet skyddas med paketeraren. Värdet får inte vara negativt. Det här alternativet kan inte användas med <span class="codeph"> -e </span>. Om du vill ta bort varaktigheten när du uppdaterar en profil använder du <span class="codeph"> -r </span> utan att ange ett antal minuter. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s datum </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Det datum efter vilket licenserna kommer att gälla. Ange som <span class="+ topic/ph pr-d/codeph codeph"> åååå-mm-dd </span> eller <span class="+ topic/ph pr-d/codeph codeph"> åååå-mm-dd-h24:min:sek </span>. Exempel: 2008-12-1 eller 2008-12-1-00:00:00 för midnatt den 1 december 2008. Värdet måste vara mindre än värdet för <span class="codeph"> -e </span>, om det finns. Det här alternativet kan inte användas med <span class="codeph"> -r </span>. Om du vill ta bort startdatumet när du uppdaterar en princip använder du <span class="codeph"> -s </span> utan att ange ett datum. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w minuter </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Uppspelningsfönstret (det antal minuter som innehållet kan visas, med början från den första uppspelningen). Om det här alternativet inte anges eller om <span class="codeph"> -w </span> används utan att ange antalet minuter finns det ingen begränsning för uppspelningsfönstret. Värdet får inte vara negativt. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l minuter </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Licensens cachelagringstid i minuter, vilket är den tidpunkt då en licens tillåts cachelagras i klientens License Store efter att licensen har utfärdats av servern. Värdet får inte vara negativt. Ange <span class="codeph"> -l 0 </span> för att ange att cache-lagring av licenser inte är tillåten. Använd <span class="codeph"> -l </span> utan att ange ett antal minuter för obegränsad licenscachelagring. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Licensens slutdatum för cachelagring (det datum efter vilket licenserna inte kan cachas i klientens License Store, efter att licensen har utfärdats av servern). Ange som <span class="+ topic/ph pr-d/codeph codeph"> åååå-mm-dd </span><i class="+ topic/ph hi-d/i "></i>eller<i class="+ topic/ph hi-d/i "> </i> åååå-mm-dd-h24:min:sek <span class="+ topic/ph pr-d/codeph codeph"> </span>. Exempel: 2008-12-1 eller 2008-12-1-00:00:00 för midnatt den 1 december 2008. Använd <span class="codeph"> -l </span> utan att ange ett antal minuter för obegränsad licenscachelagring. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Namnområdet för autentisering. Om det anges bör klienten autentisera med ett användarnamn och lösenord som utfärdats av den angivna utfärdaren. Det här alternativet kan inte användas med <span class="codeph"> -x </span>. Det är inte tillåtet för uppdateringar. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Tillåt anonym åtkomst. Det här alternativet kan inte användas med <span class="codeph"> -authNS </span>. Det är inte tillåtet för uppdateringar. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId </span>[: <span class="+ topic/ph pr-d/codeph codeph"> appId </span>[:[ <span class="+ topic/ph pr-d/codeph codeph"> min </span>]:[ <span class="+ topic/ph pr-d/codeph codeph"> max </span>]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">En lista över tillåtna AIR-program som kan spela upp skyddat innehåll. Använd det här för att begränsa vilka utgivare, program och versioner som får komma åt innehåll som skyddas med den här profilen. </p> <p class="- topic/p ">Om <i class="+ topic/ph hi-d/i ">appId</i> inte anges tillåts alla program för utgivaren <i class="+ topic/ph hi-d/i ">pubId</i> . </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">min</i> - och <i class="+ topic/ph hi-d/i ">max</i> -versionsnummer är valfria. </p> <p class="- topic/p ">Flera <span class="codeph"> -air- </span> alternativ kan anges för att tillåta flera program. Om inga AIR- eller SWF-program anges kan alla program få åtkomst till det här innehållet. Under en uppdatering använder du -air utan de återstående argumenten för att ta bort alla poster från listan. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist name </span> / <i class="+ topic/ph hi-d/i "></i> value <span class="+ topic/ph pr-d/codeph codeph"></span> <i class="+ topic/ph hi-d/i "></i> <span class="+ topic/ph pr-d/codeph codeph"> pairs </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM-klienterna hindrade åtkomst till skyddat innehåll. Värdet består av kommaavgränsade namn:värdepar med följande format: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | release= stringValue </span> </p> <p class="- topic/p ">Till exempel <span class="codeph"> os=Win,release=2.0.1 </span>. Under en uppdatering använder du <span class="codeph"> -drmBlacklist </span> utan de återstående argumenten för att ta bort alla poster från listan. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger att DRM-klienter måste ha den angivna lägsta säkerhetsnivån för att få åtkomst till skyddat innehåll. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE | KRÄVS | NO_PLAYBACK | ACP_REQUIRED | CGMS-A_REQUIRED | USE_ACP_IF_AVAILABLE | USE_CGMS-A_IF_AVAILABLE </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Begränsningar för analogt utdataskydd. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | KRÄVS | NO_PLAYBACK </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Begränsningar för skydd av digitala utdata. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist name </span> / <i class="+ topic/ph hi-d/i "></i> value <span class="+ topic/ph pr-d/codeph codeph"></span> <i class="+ topic/ph hi-d/i "></i> <span class="+ topic/ph pr-d/codeph codeph"> pairs </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Programkörningsmiljöerna hindrade från att komma åt skyddat innehåll. Värdet består av kommaavgränsade namn:värdepar med följande format: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | program | release= stringValue </span> </p> <p class="- topic/p ">Till exempel <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. Under en uppdatering använder du <span class="codeph"> -runtimeBlacklist </span> utan de återstående argumenten för att ta bort alla poster från listan. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger att programkörningsversionerna måste ha den angivna lägsta säkerhetsnivån för att få åtkomst till skyddat innehåll. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf file= swf_file </span>, <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">En lista över tillåtna SWF-program som kan spela upp skyddat innehåll. Flera -swf-alternativ kan anges för att tillåta flera program. Om inga AIR- eller SWF-program anges kan alla program få åtkomst till det här innehållet. Under en uppdatering använder du -swf utan de återstående argumenten för att ta bort alla poster från listan. Om du vill identifiera en SWF-fil med dess hash-värde anger du den SWF-fil som hash-värdet ska beräknas för och den maximala tid som SWF-verifieringen kan slutföras (i sekunder). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= värde </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger anpassade nycklar/värden som ska läggas till i profilen. Flera <span class="codeph"> -k- </span> alternativ kan anges. Använd <span class="codeph"> -k </span> utan de återstående argumenten för att ta bort alla egenskaper under uppdateringen. Det är helt upp till implementeringen av Adobe Access-licensservern att tolka eller hantera dessa data. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name= value </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Lägger till en anpassad egenskap som visas i licensen som skapas för varje klient. Flera <span class="codeph"> -p- </span> alternativ kan anges för att lägga till flera egenskaper. Under en uppdatering använder du <span class="codeph"> -p </span> utan de återstående argumenten för att ta bort alla egenskaper. Tolkningen eller hanteringen av dessa data är helt och hållet upp till implementeringen av klientapplikationen. </p> </td> 
  </tr> 
 </tbody> 
</table>

