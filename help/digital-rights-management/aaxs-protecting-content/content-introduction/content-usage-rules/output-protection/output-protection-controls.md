---
seo-title: Skydd av utdata
title: Skydd av utdata
uuid: 1f4cc617-7f14-4952-8e61-6acbdf01d10e
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# Utdataskyddskontroller {#output-protection-controls}

**Kontrollera om utdata till externa återgivningsenheter är skyddade. Ange analoga och digitala utdata oberoende av varandra.**

Anger om utdata till externa återgivningsenheter ska begränsas. En extern enhet definieras som en video- eller ljudenhet som inte är inbäddad i datorn. I listan över externa enheter ingår inte integrerade skärmar, t.ex. bärbara datorer. Begränsningar för analoga och digitala utdata kan anges oberoende av varandra.

Följande alternativ/efterlevnadsnivåer är tillgängliga:

<table frame="all" colsep="0" rowsep="1" id="adobetable_fvw_5fx_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Alternativ </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Stöds i analoga enheter </p> </th> 
   <th colname="3" class="- topic/entry entry"> <p class="- topic/p ">Stöds i digitala enheter </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Obligatoriskt</b>  - Utdataskydd för analog kopiering (ACP) eller Copy Generation Management System - analog (CGMS-A) måste aktiveras för att innehållet ska kunna spelas upp på en extern enhet. Adobe Access-klienter måste aktivera utdataskydd med hjälp av ACP eller CGMS-A. På enheter som stöder båda försöker klienterna i Adobe Access 3.0 aktivera båda. Endast en måste dock vara aktiverad för att innehållet ska kunna spelas upp. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">JA </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">JA </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Krävs</b>  förAVS - AVS-utdataskydd krävs. Uppspelning tillåts inte på CGMS-A. Adobe Access 2.0-klienter stöder inte det här alternativet. Om den anges fungerar en Adobe Access 2.0-klient som om alternativet Ingen uppspelning hade angetts. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">JA </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">CGMS-A krävs</b>  - CGMS-A-utdataskydd krävs. Uppspelning tillåts inte på AVS. Adobe Access 2.0-klienter stöder inte det här alternativet. Om den anges fungerar en Adobe Access 2.0-klient som om alternativet Ingen uppspelning hade angetts. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">JA </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Använd om tillgängligt</b>  - Försök att aktivera AVS- och CGMS-A-utdataskydd om det är tillgängligt och tillåt uppspelning om det inte är tillgängligt. Klienter med Adobe Access 3.0 kommer att försöka aktivera både ACP och CGMS-A om möjligt. Adobe Access 2.0-klienter försöker bara aktivera antingen AVS eller CGMS-A. Adobe Access-klienten kommer till exempel att försöka aktivera antingen ACP eller CGMS-A. Om försöket lyckas aktiveras inte det andra alternativet. Om försöket misslyckas görs ett andra försök att aktivera det andra alternativet. Även om båda försöken misslyckas spelas innehållet ändå upp. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">JA </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">JA </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Använd ACP om det är tillgängligt</b>  - Försök att aktivera AVS-utdataskydd om det är tillgängligt, men tillåt uppspelning om det inte är tillgängligt. Skydd är inte tillgängligt på CGMS-A. Adobe Access 2.0-klienter stöder inte det här alternativet. Om detta anges fungerar en Adobe Access 2.0-klient som om alternativet "Inget skydd" angavs. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">JA </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Använd CGMS-A om det är tillgängligt  </b>- Försök att aktivera CGMS-A-utdataskydd om det är tillgängligt, men tillåt uppspelning om det inte är tillgängligt. Skydd är inte tillgängligt på AVS. Adobe Access 2.0-klienter stöder inte det här alternativet. Om detta anges fungerar en Adobe Access 2.0-klient som om alternativet "Inget skydd" angavs. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">JA </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Inget skydd</b>  - Ingen aktivering av utdataskydd krävs för analoga och digitala utdata. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">JA </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">JA </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Ingen uppspelning</b>  - Tillåt inte uppspelning till en extern enhet för analoga och digitala utdata. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">JA </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">JA </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Dessa regler används konsekvent på alla plattformar, men för närvarande går det bara att på ett säkert sätt aktivera utdataskydd på Windows-plattformar. På andra plattformar (till exempel Macintosh och Linux) finns det inga operativsystemsfunktioner som stöds tillgängliga för tredjepartsprogram.

Exempel: En del innehåll kan framtvinga utdataskyddskontroller och skyddsnivån kan anges av innehållsdistributören. Om&quot;Obligatoriskt&quot; har angetts och uppspelningsförsök görs på en Macintosh spelas inte innehållet upp på externa enheter. Innehållet spelas dock upp på interna bildskärmar.

Om&quot;Obligatoriskt&quot; anges och uppspelningsförsök görs på Linux, spelas inte innehållet upp på någon enhet eftersom det inte går att skilja mellan interna och externa enheter.

Om du anger &quot;Använd om tillgängligt&quot; aktiveras utdataskyddet där det är möjligt. På Windows-datorer med stöd för Certified Output Protection Protocol (COPP) skickas innehållet med utdataskydd till en extern skärm. Det här exemplet kallas ibland för&quot;valbar utdatakontroll&quot;.
