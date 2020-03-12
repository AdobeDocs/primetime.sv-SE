---
seo-title: Leverantörsspecifik säkerhetsinformation
title: Leverantörsspecifik säkerhetsinformation
uuid: 23186770-c73a-4802-bc30-fa9e4b47d9ba
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Leverantörsspecifik säkerhetsinformation{#vendor-specific-security-information}

Det här avsnittet innehåller säkerhetsrelaterad information om operativsystem och programservrar som ingår i din Adobe Access-lösning.

Använd länkarna i det här avsnittet för att hitta leverantörsspecifik säkerhetsinformation för ditt operativsystem och din programserver.

## Säkerhetsinformation för operativsystem {#section-B6D9D6CEA7CC42A8A20346600EFB5E4E}

När du skyddar ditt operativsystem ska du noga implementera de åtgärder som beskrivs av din operativsystemsleverantör, inklusive följande:

* Definiera och styra användare, roller och behörigheter
* Övervaka loggar och åtkomsthistorik
* Onödiga tjänster och program tas bort
* Säkerhetskopiera filer

Säkerhetsinformation om operativsystem som stöds i Adobe Access finns i resurserna i den här tabellen.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-ugl-kjz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Operativsystem </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Säkerhetsresurs </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Microsoft® Windows Server® 2008 Enterprise eller Standard Edition </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Säkerhetshandbok för Windows Server 2008</i> </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Red Hat® Enterprise Linux® 5.4, 5.5 och 5.6. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Red Hat Enterprise Linux 5 Security Guide</i> </p> </td> 
  </tr> 
 </tbody> 
</table>

I följande tabell beskrivs några möjliga strategier för att minimera säkerhetsbrister som finns i operativsystemet.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-whl-kjz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Objekt </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Beskrivning </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Säkerhetsuppdateringar </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Det finns en ökad risk för att en obehörig användare får åtkomst till programservern om leverantörens säkerhetsuppdateringar och uppgraderingar inte tillämpas i tid. Testa säkerhetsuppdateringar innan du använder dem på produktionsservrar. </p> <p class="- topic/p ">Du kan också skapa principer och procedurer för att regelbundet kontrollera och installera korrigeringsfiler. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Virusskydd </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Virusskannrar kan identifiera infekterade filer genom att skanna efter en signatur eller genom att titta efter ovanligt beteende. Skannrar sparar sina virussignaturer i en fil som vanligtvis lagras på den lokala hårddisken. Eftersom nya virus upptäcks ofta måste du ofta uppdatera den här filen för att virusskannern ska kunna identifiera alla aktuella virus. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">NTP (Network Time Protocol) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">För både korrekt drift och kriminalteknisk analys bör du hålla rätt tid på Adobe Access-servrar och Adobe Access-paket. Använd en säker version av NTP för att synkronisera tiden på alla system som är anslutna till Internet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Säkerhetsinformation för programserver {#section-EBB4EF371CFF4A848694CC240B23D404}

När du skyddar programservern måste du implementera de mått som beskrivs av serverleverantören, inklusive följande:

* Använda ett användarnamn som inte är uppenbart för administratören
* Onödiga tjänster inaktiveras
* Skydda konsolhanteraren
* Aktivera säkra cookies
* Stänger portar som inte behövs
* Begränsa administrativa gränssnitt med IP-adresser eller domäner
* Använda Java™ Security Manager

