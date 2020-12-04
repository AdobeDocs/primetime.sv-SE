---
description: HLS- och DASH-strömmar ger olika bithastighetskodningar (profiler) för samma korta videosekvens. TVSDK kan välja kvalitetsnivå för varje explosion baserat på tillgänglig bandbredd.
seo-description: HLS- och DASH-strömmar ger olika bithastighetskodningar (profiler) för samma korta videosekvens. TVSDK kan välja kvalitetsnivå för varje explosion baserat på tillgänglig bandbredd.
seo-title: Adaptiva bithastigheter (ABR) för videokvalitet
title: Adaptiva bithastigheter (ABR) för videokvalitet
uuid: e5752d7e-fa7d-407c-96df-c3830a35c66e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---


# Adaptiva bithastigheter (ABR) för videokvalitet{#adaptive-bit-rates-abr-for-video-quality}

HLS- och DASH-strömmar ger olika bithastighetskodningar (profiler) för samma korta videosekvens. TVSDK kan välja kvalitetsnivå för varje explosion baserat på tillgänglig bandbredd.

TVSDK övervakar hela tiden bithastigheten för att säkerställa att innehållet spelas upp med den optimala bithastigheten för den aktuella nätverksanslutningen.

Du kan ange den adaptiva byteprincipen för bithastighet (ABR) och den inledande, lägsta och högsta bithastigheten för en MBR-ström (Multiple-bit rate). TVSDK växlar automatiskt till den bithastighet som ger den bästa uppspelningsupplevelsen i den angivna konfigurationen.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Inledande bithastighet </td> 
   <td colname="col2"> <p>Den önskade uppspelningsbithastigheten (i bitar per sekund) för det första segmentet. När uppspelningen startar används den närmaste profilen, som är lika med eller större än den ursprungliga bithastigheten, för det första segmentet. </p> <p> Om en lägsta bithastighet definieras och den inledande bithastigheten är lägre än den lägsta hastigheten, väljer TVSDK profilen med den lägsta bithastigheten över den lägsta bithastigheten. Om den inledande räntan ligger över den högsta nivån väljer TVSDK den högsta nivån under den högsta nivån. </p> <p>Om den inledande bithastigheten är noll eller odefinierad bestäms den inledande bithastigheten av ABR-principen. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Minsta bithastighet </td> 
   <td colname="col2"> <p>Den lägsta tillåtna bithastigheten som ABR kan växla till. ABR-växling ignorerar profiler med en bithastighet som är lägre än denna bithastighet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Maximal bithastighet </td> 
   <td colname="col2"> <p>Den högsta tillåtna bithastighet som ABR kan växla till. ABR-växling ignorerar profiler med en bithastighet som är högre än den här bithastigheten. </p> </td> 
  </tr> 
 </tbody> 
</table>

Tänk på följande:

* TVSDK skickar inte händelser från växling av bithastighet.
* Du kan ändra ABR-inställningarna när som helst, och spelaren växlar till den profil som mest liknar de senaste inställningarna.

Om en ström till exempel har följande profiler:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Om du anger ett intervall på 300000 till 2000000 kommer TVSDK endast att ta hänsyn till profilerna 1, 2 och 3. Detta gör att program kan justeras till olika nätverksförhållanden, som att växla från WiFi till 3G eller till olika enheter som en telefon, en surfplatta eller en stationär dator.

## Konfigurera adaptiva bithastigheter {#section_572FCE4CC28D4DF8BD9C461F00B3CA17}

Så här konfigurerar du adaptiva bithastighetsparametrar för TVSDK:

1. Konfigurera en instans av `PTABRControlParameters` för att ange inställningar för inledande, lägsta och högsta bithastighet.

   Standardvärdena visas i följande kodfragment, men programmet kan ange ett heltalsvärde för var och en av dessa parametrar.

   >[!IMPORTANT]
   >
   >Ange bithastighetsinställningarna i bitar per sekund (bps).

   ```
   // ARC (add autorelease for non-ARC) 
   PTABRControlParameters *abrMetaData =  
       [[PTABRControlParameters alloc] init];  
   
   abrMetaData.initialBitRate = -1; 
   abrMetaData.minBitRate = 0; 
   abrMetaData.maxBitRate = INT_MAX;
   ```

1. Uppdatera din `PTMediaPlayer`-instans med den konfigurerade `PTABRControlParameters`-instansen.

   ```
   // assuming self.player is the PTMediaPlayer instance 
   self.player.abrControlParameters = abrMetaData;
   ```

Kom ihåg följande:

* Programmet måste ställa in egenskapen `abrControlParameters` på `PTMediaPlayer` innan en `PTMediaPlayerItem`-instans konfigureras för att de inledande och lägsta bithastighetsinställningarna ska börja gälla.

   När uppspelningen av innehållet startar påverkas inställningen för en ny instans bara den maximala bithastigheten.

* Om du vill uppdatera den maximala bithastighetsinställningen under uppspelning skapar du en ny `PTABRControlParameters`-instans och anger den på spelarinstansen.
* Du kan bara uppdatera inställningen för högsta bithastighet under uppspelning på iOS 8.0 och senare. I tidigare versioner används det `maxBitrate`-värde som angavs innan innehållsuppspelningen startades.

