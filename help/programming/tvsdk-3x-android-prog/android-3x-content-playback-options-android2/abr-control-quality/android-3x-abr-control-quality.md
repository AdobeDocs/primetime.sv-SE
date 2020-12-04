---
description: HLS- och DASH-strömmar ger olika bithastighetskodningar (profiler) för samma korta videosekvens. TVSDK kan välja kvalitetsnivå för varje explosion baserat på den aktuella buffertnivån och den tillgängliga bandbredden.
seo-description: HLS- och DASH-strömmar ger olika bithastighetskodningar (profiler) för samma korta videosekvens. TVSDK kan välja kvalitetsnivå för varje explosion baserat på den aktuella buffertnivån och den tillgängliga bandbredden.
seo-title: Adaptiva bithastigheter (ABR) för videokvalitet
title: Adaptiva bithastigheter (ABR) för videokvalitet
uuid: 87fd7d97-8d13-430d-a88e-bcbff8026679
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---


# Översikt {#adaptive-bit-rates-abr-for-video-quality-overview}

HLS- och DASH-strömmar ger olika bithastighetskodningar (profiler) för samma korta videosekvens. TVSDK kan välja kvalitetsnivå för varje explosion baserat på den aktuella buffertnivån och den tillgängliga bandbredden.

TVSDK övervakar hela tiden bithastigheten för att säkerställa att innehållet spelas upp med den optimala bithastigheten för den aktuella nätverksanslutningen. Du kan ange den adaptiva byteprincipen för bithastighet (ABR) och den inledande, lägsta och högsta bithastigheten för en MBR-ström (Multiple-bit rate). TVSDK växlar automatiskt till den bithastighet som ger den bästa uppspelningsupplevelsen i den angivna konfigurationen.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Inledande bithastighet </td> 
   <td colname="col2"> <p>Den önskade uppspelningsbithastigheten (i bitar per sekund) för det första segmentet. </p> <p>När uppspelningen startar används den närmaste profilen, som är lika med eller större än den ursprungliga bithastigheten, för det första segmentet. Om en lägsta bithastighet definieras och den inledande bithastigheten är lägre än den lägsta hastigheten, väljer TVSDK profilen med den lägsta bithastigheten över den lägsta bithastigheten. Om den inledande räntan ligger över den högsta nivån väljer TVSDK den högsta nivån under den högsta nivån. Om den inledande bithastigheten är noll eller odefinierad bestäms den inledande bithastigheten av ABR-principen. </p> <p><span class="codeph"> </span> getABRInitialBitRatern returnerar ett heltalsvärde som representerar byteprofilen per sekund. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Minsta bithastighet </td> 
   <td colname="col2"> <p>Den lägsta tillåtna bithastigheten som ABR kan växla till. </p> <p>ABR-växling ignorerar profiler med en bithastighet som är lägre än denna bithastighet. <span class="codeph"> </span> getABRMinBitRatern returnerar ett heltalsvärde som representerar bitprofilen per sekund. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Maximal bithastighet </td> 
   <td colname="col2"> <p>Den högsta tillåtna bithastighet som ABR kan växla till. </p> <p>ABR-växling ignorerar profiler med en bithastighet som är högre än den här bithastigheten. <span class="codeph"> </span> getABRMaxBitRatern returnerar ett heltalsvärde som representerar bitprofilen per sekund. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR-växlingsprincip </td> 
   <td colname="col2"> <p>Uppspelningen växlar gradvis till den högsta bithastigheten när det är möjligt. Du kan ange en princip för ABR-växling, som avgör hur snabbt TVSDK växlar mellan profiler. Standardvärdet är <span class="codeph"> ABR_MODERATE</span>. </p> <p>När TVSDK bestämmer sig för att byta till en högre bithastighet väljer spelaren den idealiska bithastighetsprofilen att växla till baserat på den aktuella ABR-principen: 
     <ul id="ul_AC9C99D84A3B4A8DBD1A05CC05DEE771"> 
      <li id="li_B79C0AA2CBFB42FF98A257CEC9C400BA"><span class="codeph"> ABR_CONSERVATIVE</span>: Växlar till profilen med nästa högre bithastighet när bandbredden är 50 % högre än den aktuella bithastigheten. </li> 
      <li id="li_38CC3A95D8634F359D0F7C273D0108C0"><span class="codeph"> ABR_MODERATE</span>: Växlar till nästa högre bithastighetsprofil när bandbredden är 20 % högre än den aktuella bithastigheten. </li> 
      <li id="li_E845C035420D4B3FB2B179F448F8CA85"><span class="codeph"> ABR_AGGRESSIVE</span>: Växlar omedelbart till den högsta bithastighetsprofilen när bandbredden är högre än den aktuella bithastigheten. </li> 
     </ul> </p> <p>Om den inledande bithastigheten är noll, eller inte har angetts, men en princip har angetts, startar uppspelningen med den lägsta bithastighetsprofilen för en konservativ princip, den profil som ligger närmast mediandbithastigheten för tillgängliga profiler för en måttlig princip och den högsta bithastighetsprofilen för en aggressiv princip. </p> <p>Principen fungerar i begränsningarna för lägsta och högsta bithastighet, om dessa hastigheter anges. </p> <p> <span class="codeph"> </span> getABRPolicyreturnerar den aktuella inställningen från  <span class="codeph"> </span> ABRControlParametersenum:  <span class="codeph"> ABR_CONSERVATIVE</span>,  <span class="codeph"> ABR_MODERATE</span> eller  <span class="codeph"> ABR_AGGRESSIVE</span>. </p> <p>Mer information finns i ABR Control Parameters API doc. </p> </td> 
  </tr> 
 </tbody> 
</table>

Tänk på följande:

* Felväxlingsmekanismen för TVSDK kan åsidosätta dina inställningar eftersom TVSDK prioriterar en kontinuerlig uppspelning framför att strikt följa dina kontrollparametrar.
* När bithastigheten ändras skickar TVSDK `onProfileChanged`-händelser i `PlaybackEventListener`.

* Du kan ändra ABR-inställningarna när som helst, och spelaren växlar till den profil som mest liknar de senaste inställningarna.

Om en ström till exempel har följande profiler:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Om du anger ett intervall på 300000 till 2000000 kommer TVSDK endast att ta hänsyn till profilerna 1, 2 och 3. Detta gör att program kan justeras till olika nätverksförhållanden, t.ex. växla från Wi-Fi till 3G eller till olika enheter som en telefon, en surfplatta eller en stationär dator.

Om du vill ange ABR-kontrollparametrar anger du parametrarna för klassen `ABRControlParameter`.