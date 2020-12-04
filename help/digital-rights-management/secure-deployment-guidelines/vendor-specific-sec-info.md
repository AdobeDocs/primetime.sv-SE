---
description: Operativsystem och programservrar ingår i Adobe Primetime DRM-lösning.
seo-description: Operativsystem och programservrar ingår i Adobe Primetime DRM-lösning.
seo-title: Leverantörsspecifik säkerhetsinformation
title: Leverantörsspecifik säkerhetsinformation
uuid: 331baa42-5e19-40a5-bc74-0b1a2cb9370e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---


# Leverantörsspecifik säkerhetsinformation{#vendor-specific-security-information}

Operativsystem och programservrar ingår i Adobe Primetime DRM-lösning.

Information om leverantörsspecifik säkerhetsinformation för ditt operativsystem och din programserver finns i Använda nyckelservern för Adobe Primetime DRM.

## Säkerhetsinformation för operativsystem {#section_53CAD802FCA54C4D8CE0C4E1B3045E52}

När du skyddar ditt operativsystem måste du implementera de mått som beskrivs av din operativsystemsleverantör.

Här är några av åtgärderna:

* Definiera och styra användare, roller och behörigheter
* Övervaka loggar och åtkomsthistorik
* Onödiga tjänster och program tas bort
* Säkerhetskopiera filer

Här är information om de operativsystem som stöds av Adobe Primetime DRM:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ugl_kjz_n4"> 
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

Här följer information om strategier för att minimera säkerhetsluckor i operativsystemet:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_whl_kjz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Objekt </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Beskrivning </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Säkerhetsuppdateringar </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Det finns en ökad risk för att en obehörig användare får åtkomst till programservern om leverantörens säkerhetsuppdateringar och uppgraderingar inte tillämpas i tid. </p> <p>Obs!  Kontrollera att du testar säkerhetsuppdateringar innan du använder dem på produktionsservrar. </p> <p class="- topic/p ">Du måste skapa principer och procedurer för att regelbundet söka efter och installera korrigeringsfiler. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Virusskydd </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Virusskannrar kan identifiera infekterade filer genom att söka efter en signatur eller ovanliga beteenden. </p> <p>Skannrar sparar sina virussignaturer i en fil som vanligtvis lagras på den lokala hårddisken. Nya virus upptäcks ofta, så du måste se till att filen uppdateras regelbundet. På så sätt kan virusskannrar alltid identifiera alla aktuella virus. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">NTP (Network Time Protocol) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">För att få en korrekt funktion och kriminalteknisk analys bör du hålla rätt tid på Primetimes DRM-servrar och -paketerare. Använd en säker version av NTP för att synkronisera Primetime DRM-tiden på alla system som är anslutna till Internet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Säkerhetsinformation för programserver {#section_22986936F1A547CEAB2D97E9E9D4825C}

När du skyddar programservern måste du implementera de mått som beskrivs av serverleverantören.

Här är några av dessa åtgärder:

* Använda ett användarnamn som inte är uppenbart för administratören
* Onödiga tjänster inaktiveras
* Skydda konsolhanteraren
* Aktivera säkra cookies
* Stänger portar som inte behövs
* Begränsa administrativa gränssnitt med IP-adresser eller domäner
* Använda Java™ Security Manager

