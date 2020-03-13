---
seo-title: Egenskaper för konfigurationsfil
title: Egenskaper för konfigurationsfil
uuid: 13e158a6-c447-4e5e-884d-03fb4835c120
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Egenskaper för konfigurationsfil {#configuration-file-properties}

Innan du kör licensgeneratorn anger du värden för licensgeneratoregenskaperna. Konfigurationsfilen anger följande egenskaper. För egenskapsnamn som innehåller *n* representerar *n* ett heltal som börjar med 1 och ökar för varje instans av egenskapen.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_qk1_rry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Egenskap </th> 
   <th colname="2" class="- topic/entry entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.minClientVersion</span> </td> 
   <td colname="2" class="- topic/entry "> Ange den lägsta klientversion som stöds. Om den inte anges stöds alla versioner som standard. Ange det här värdet för att kontrollera hur äldre klienter svarar på licenskrav som de inte stöder. Ange x (för Adobe Access x.0) där x är det största versionsnumret. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Key Server-certifikat (ett Adobe-utfärdat licensservercertifikat som används av Key Server). Det här certifikatet används endast om metadata/principen anger att en nyckelserver krävs för nyckelleverans till iOS-enheter. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> PKCS12-filen som innehåller autentiseringsuppgifterna för licensservern för undertecknande av licenser. Den här egenskapen bör referera till en pfx-fil som innehåller ett certifikat och en privat nyckel. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">Lösenordet som används för att skydda filen som anges av <span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile.</span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> Om domänbundna licenser genereras måste ett eller flera certifikat för domänkontrollant anges för att ange vilka domänmyndigheter som är betrodda av den här licensutfärdaren. Om licensmottagaren är ett domäncertifikat som inte har utfärdats av någon av de angivna domänkontrollanterna går det inte att generera någon licens. This property specifies a .cer file that contains the certificate only (either PEM or DER format is acceptable). n måste öka monotont, med början från 1. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymmetric.licenseServerCredential.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Valfri PKCS12-fil med ytterligare autentiseringsuppgifter för licensservern för dekryptering av CEK i metadata och principen. Ytterligare autentiseringsuppgifter kan konfigureras om innehållet tidigare paketerats med ett annat licensservercertifikat än det som anges av <span class="codeph"> licensegen.sign.certfile</span>. Den här egenskapen bör referera till en <span class="filepath"> .pfx</span> -fil som innehåller ett certifikat och en privat nyckel. n måste öka monotont, med början från 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymmetric.licenseServerCredential.n.password</span> </td> 
   <td colname="2" class="- topic/entry ">Lösenordet som används för att skydda filen som anges av: <p><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.asymmetric.licenseServerCredential.n</span> </p> </td> 
  </tr> 
 </tbody> 
</table>

