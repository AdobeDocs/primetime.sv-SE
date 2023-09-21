---
description: HLS- och DASH-strömmar ger olika bithastighetskodningar (profiler) för samma korta videosekvens. TVSDK kan välja kvalitetsnivå för varje explosion baserat på tillgänglig bandbredd.
title: Adaptiva bithastigheter (ABR) för videokvalitet
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '973'
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
   <td colname="col2"> <p>Uppspelningens önskade bithastighet (i bitar per sekund) för det första segmentet. När uppspelningen startar används den närmaste profilen, som är lika med eller större än den ursprungliga bithastigheten, för det första segmentet. </p> <p> Om en lägsta bithastighet definieras och den inledande bithastigheten är lägre än den lägsta hastigheten, väljer TVSDK profilen med den lägsta bithastigheten över den lägsta bithastigheten. Om den inledande räntan ligger över den högsta nivån väljer TVSDK den högsta nivån under den högsta nivån. </p> <p>Om den inledande bithastigheten är noll eller odefinierad bestäms den inledande bithastigheten av ABR-principen. </p> <p> <span class="apiname"> ABRInitialBitRate </span> returnerar ett heltalsvärde som representerar byteprofilen per sekund. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Minsta bithastighet </td> 
   <td colname="col2"> <p>Den lägsta tillåtna bithastigheten som ABR kan växla till. ABR-växling ignorerar profiler med en bithastighet som är lägre än denna bithastighet. </p> <p> <span class="apiname"> ABRMinBitRate </span> returnerar ett heltalsvärde som representerar profilen bitar per sekund. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Maximal bithastighet </td> 
   <td colname="col2"> <p>Den högsta tillåtna bithastighet som ABR kan växla till. ABR-växling ignorerar profiler med en bithastighet som är högre än denna bithastighet. </p> <p> <span class="apiname"> ABRMaxBitRate </span> returnerar ett heltalsvärde som representerar profilen bitar per sekund. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR-växlingsprincip </td> 
   <td colname="col2"> Uppspelningen växlar gradvis till den högsta bithastigheten när det är möjligt. Du kan ange en princip för ABR-växling, som avgör hur snabbt TVSDK växlar mellan profiler. Standardvärdet är <span class="codeph"> MODERATE_POLICY </span>. <p>När TVSDK bestämmer sig för att byta till en högre bithastighet väljer spelaren den idealiska bithastighetsprofilen att växla till baserat på den aktuella ABR-principen: 
     <ul id="ul_058D0FFC944C476A83BB9E756B95DEBD"> 
      <li id="li_C690A12DC34C4754B01C2D0616FB6A0A"> <span class="codeph"> CONSERVATIVE_POLICY </span>: Växlar till profilen med nästa högre bithastighet när bandbredden är 50 % högre än den aktuella bithastigheten. </li> 
      <li id="li_FF5BDB099B554940AC296938C7A12B81"> <span class="codeph"> MODERATE_POLICY </span>: Växlar till nästa högre bithastighetsprofil när bandbredden är 20 % högre än den aktuella bithastigheten. </li> 
      <li id="li_E602508429864C279BF78360E95718A6"> <span class="codeph"> AGGRESSIVE_POLICY </span>: Växlar omedelbart till den högsta bithastighetsprofilen när bandbredden är högre än den aktuella bithastigheten. </li> 
     </ul> </p> <p>Om den inledande bithastigheten är noll eller inte har angetts, men en princip har angetts, startar uppspelningen med den lägsta bithastighetsprofilen för konservativ, den profil som ligger närmast mediandbithastigheten för tillgängliga profiler för måttlig och den högsta bithastighetsprofilen för aggressiv. </p> <p>Principen fungerar i begränsningarna för lägsta och högsta bithastighet, om dessa hastigheter anges. </p> <p> <span class="codeph"> ABRPolicy </span> returnerar den aktuella inställningen från <span class="codeph"> ABRControlParameters </span> enum: CONSERVATIVE_POLICY, MODERATE_POLICY eller AGGRESSIVE_POLICY. </p> </td> 
  </tr> 
 </tbody> 
</table>

Tänk på följande:

* Felväxlingsmekanismen för TVSDK kan åsidosätta dina inställningar eftersom TVSDK prioriterar en kontinuerlig uppspelning framför att strikt följa dina kontrollparametrar.
* När bithastigheten ändras skickas TVSDK `ProfileEvent.PROFILE_CHANGED`.
* Du kan ändra ABR-inställningarna när som helst, och spelaren växlar till den profil som mest liknar de senaste inställningarna.

Om en ström till exempel har följande profiler:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Om du anger ett intervall på 300000 till 2000000 kommer TVSDK endast att ta hänsyn till profilerna 1, 2 och 3. Detta gör att program kan justeras till olika nätverksförhållanden, t.ex. växla från Wi-Fi till 3G eller till olika enheter som en telefon, en surfplatta eller en stationär dator.

Gör något av följande om du vill ange ABR-kontrollparametrar:

* Använd `ABRControlParameterBuilder` hjälpklass för att ställa in en delmängd av parametrarna (arbetar på `ABRControlParameter` bakom kulisserna)

* Ange parametrarna på `ABRControlParameter` klassen.

## Konfigurera adaptiva bithastigheter med ABRControlParametersBuilder {#section_3DDE397A7CE445E1832EBAA46CE5C069}

Använda `ABRControlParametersBuilder` hjälpklass är det enklaste och effektivaste sättet att ställa in ABR-parametrar.

* The `ABRControlParametersBuilder` konstruktorn ställer in alla ABR-parametrar till standardvärden för den underliggande `ABRControlParameters` -objekt.

* Du kan återställa enskilda ABR-parametrar under körning, förutsatt att du behåller en referens till samma `ABRControlParametersBuilder` -instans.

Den här klassen innehåller även `toABRControlParameters()` hjälpmetod. Använd den här metoden för att hämta en instans av `ABRControlParameters` och på `mediaPlayer.ABRControlParameters` -egenskap. Detta gör att inställningarna börjar gälla i spelaren.

1. Instansiera `ABRControlParametersBuilder` hjälpklass och ange parametrar för Media Player.

   >[!NOTE]
   >
   >I följande exempel initieras alla parametrar till standardvärdena, och sedan anges endast principen till konservativ och den maximala bithastigheten begränsas till 100000:
   >
   >```
   >var abrBuilder:ABRControlParametersBuilder =  
   >   new ABRControlParametersBuilder(); 
   >abrBuilder.policy = ABRControlParameters.CONSERVATIVE_POLICY; 
   >abrBuilder.maxBitRate = 1000000; 
   >mediaPlayer.abrControlParameters =  
   >   abrBuilder.toABRControlParameters();
   >```
   >

1. Ändra enskilda ABR-parametrar vid körning.

   Så här ändrar du enskilda parametrar utan att låta resten av parametrarna vara som de var:

   ```
   // If later you want to reset the max bit rate to 2000000 
   abrBuilder.maxBitRate = 2000000; 
   mediaPlayer.abrControlParameters =  
     abrBuilder.toABRControlParameters();
   ```

   Om du vill behålla dina tidigare inställningar måste du ha en referens till samma `ABRControlParametersBuilder` -instans som du skapade i steg 1.

## Konfigurera adaptiva bithastigheter med ABRControlParameters {#section_02161FD0A73F40ED9CAE17F9AF850483}

Du kan bara ange ABR-kontrollvärden med `ABRControlParameters`, men du kan när som helst skapa en ny.

Möjligheten att ställa in ABR-parametrar stöddes innan `ABRControlParametersBuilder` -klass, men den här möjligheten är fortfarande effektiv för att ställa in ABR-parametrar under konstruktionsfasen. Om du vill ändra enskilda parametrar efter konstruktionen bör du använda `ABRControlParametersBuilder` klassen.

Följande villkor gäller för `ABRControlParameters`:

* Du måste ange värden för alla parametrar under konstruktionstiden.
* Du kan inte ändra enskilda värden efter byggtiden.
* Om parametrarna som du anger ligger utanför det tillåtna intervallet kan du `ArgumentError` kastas.

1. Bestäm den inledande, lägsta och högsta bithastigheten.
1. Bestäm ABR-principen:

   * `CONSERVATIVE_POLICY`
   * `MODERATE_POLICY`
   * `AGGRESSIVE_POLICY`

1. Ange ABR-parametervärden i dialogrutan `ABRControlParameters` och tilldela dem till Media Player.

   ```
   mediaPlayer.abrControlParameters = new ABRControlParameters( 
       ABRControlParameters.CONSERVATIVE_POLICY, 
       0, // Initial bit rate 
       0, // Minimum bit rate 
       1000000 // Maximum bit rate 
   );
   ```
