---
description: HLS- och DASH-strömmar ger olika bithastighetskodningar (profiler) för samma korta videosekvens. Webbläsare-TVSDK kan välja kvalitetsnivå för varje explosion baserat på tillgänglig bandbredd.
seo-description: HLS- och DASH-strömmar ger olika bithastighetskodningar (profiler) för samma korta videosekvens. Webbläsare-TVSDK kan välja kvalitetsnivå för varje explosion baserat på tillgänglig bandbredd.
seo-title: Adaptiva bithastigheter (ABR) för videokvalitet
title: Adaptiva bithastigheter (ABR) för videokvalitet
uuid: 4c34fb7b-1bbd-4fa9-8929-d50e85a17396
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---


# Översikt {#adaptive-bit-rates-abr-for-video-quality-overview}

HLS- och DASH-strömmar ger olika bithastighetskodningar (profiler) för samma korta videosekvens. Webbläsare-TVSDK kan välja kvalitetsnivå för varje explosion baserat på tillgänglig bandbredd.

Browser TVSDK övervakar hela tiden bithastigheten för att säkerställa att innehållet spelas upp med den optimala bithastigheten för den aktuella nätverksanslutningen.

Du kan ange den adaptiva byteprincipen för bithastighet (ABR) och den inledande, lägsta och högsta bithastigheten för en MBR-ström (Multiple-bit rate). Browser TVSDK växlar automatiskt till den bithastighet som ger den bästa uppspelningsupplevelsen i den angivna konfigurationen.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Inledande bithastighet </td> 
   <td colname="col2">Den önskade uppspelningsbithastigheten (i bitar per sekund) för det första segmentet. När uppspelningen startar används den närmaste profilen, som är lika med eller större än den ursprungliga bithastigheten, för det första segmentet. <p> Om en lägsta bithastighet har definierats och den inledande bithastigheten är lägre än minimihastigheten, väljer webbläsaren TVSDK profilen med den lägsta bithastigheten över den lägsta bithastigheten. Om den inledande hastigheten är högre än den högsta nivån väljer webbläsaren TVSDK den högsta nivån under den högsta. </p> <p>Om den inledande bithastigheten är noll eller odefinierad bestäms den inledande bithastigheten av ABR-principen. </p> <p><span class="codeph"> </span> initialBitRatern returnerar ett heltalsvärde som representerar byte-per-sekund-profilen. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Minsta bithastighet </td> 
   <td colname="col2">Den lägsta tillåtna bithastigheten som ABR kan växla till. ABR-växling ignorerar profiler med en bithastighet som är lägre än denna bithastighet. <p><span class="codeph"> </span> minBitRatern returnerar ett heltalsvärde som representerar profilen bitar per sekund. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Maximal bithastighet </td> 
   <td colname="col2">Den högsta tillåtna bithastighet som ABR kan växla till. ABR-växling ignorerar profiler med en bithastighet som är högre än den här bithastigheten. <p><span class="codeph"> </span> maxBitRatern returnerar ett heltalsvärde som representerar bitprofilen per sekund. </p> </td> 
  </tr> 
 </tbody> 
</table>

Tänk på följande:

* När bithastigheten ändras skickar webbläsaren TVSDK `AdobePSDK.ProfileEvent` med typen `AdobePSDK.PSDKEventType.PROFILE_CHANGED`.

* Du kan ändra ABR-inställningarna när som helst, och spelaren växlar till den profil som mest liknar de senaste inställningarna.

Om en ström till exempel har följande profiler:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Om du anger ett intervall på 300000 till 2000000 kommer webbläsarens TVSDK endast att hantera profilerna 1, 2 och 3. Detta gör att program kan justeras till olika nätverksförhållanden, t.ex. växla från Wi-Fi till 3G eller till olika enheter som en telefon, en surfplatta eller en stationär dator.

Så här anger du ABR-kontrollparametrar:

* Ange parametrarna för klassen `ABRControlParameters`.

