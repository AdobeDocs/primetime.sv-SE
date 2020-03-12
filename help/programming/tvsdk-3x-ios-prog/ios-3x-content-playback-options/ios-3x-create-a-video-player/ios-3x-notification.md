---
description: Spelaren kan lyssna efter en rad händelser som anger spelarens tillstånd.
seo-description: Spelaren kan lyssna efter en rad händelser som anger spelarens tillstånd.
seo-title: Konfigurera meddelanden
title: Konfigurera meddelanden
uuid: b178b2eb-da40-456b-997a-46ae18d635fa
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Konfigurera meddelanden {#set-up-notifications}

Spelaren kan lyssna efter en rad händelser som anger spelarens tillstånd.

Om det `PTMediaPlayer` är en egenskap för klientspelaren representerar `self.player` i följande exempel `PTMediaPlayer` instansen. I följande exempel implementeras den metod `addObservers` som visas i instruktionerna för konfiguration av PTMediaPlayer och de flesta meddelanden ingår:

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerStatusChange:)  
      name:PTMediaPlayerStatusNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
      name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerTimeChange:)  
      name:PTMediaPlayerTimeChangeNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerItemPlayStarted:)  
      name:PTMediaPlayerPlayStartedNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerItemPlayCompleted:)  
      name:PTMediaPlayerPlayCompletedNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerItemTimelineChanged:)  
      name:PTMediaPlayerTimelineChangedNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
      name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakStarted:)  
      name:PTMediaPlayerAdBreakStartedNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakCompleted:)  
      name:PTMediaPlayerAdBreakCompletedNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdPlayStarted:)  
      name:PTMediaPlayerAdStartedNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdPlayProgress:)  
      name:PTMediaPlayerAdProgressNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdPlayCompleted:)  
      name:PTMediaPlayerAdCompletedNotification object:self.player]; 
```

## iOS-meddelanden {#section_65D9B2DBF5574313BD3218AB02242BBB}

`ThePTMediaPlayerNotifications` -klassen visar de meddelanden som TVSDK skickar till din spelare.

<table frame="all" colsep="1" rowsep="1" id="table_ios_notifications"> 
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Meddelande</b> </td> 
   <td colname="2"> <b>Betydelse</b> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerAdBreakCompletedNotification </span> </td> 
   <td colname="2"> En annonsbrytning tog slut. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerAdBreakStartedNotification </span> </td> 
   <td colname="2"> En annonsbrytning började. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerAdClickNotification </span> </td> 
   <td colname="2"> En användare klickade på en banners. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerAdCompletedNotification </span> </td> 
   <td colname="2"> En enskild annons slutade. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerAdProgressNotification </span> </td> 
   <td colname="2"> En annons fortskrider. skickas kontinuerligt medan en annons spelas upp. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerAdStartedNotification </span> </td> 
   <td colname="2"> En enskild annons började. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTBackgroundManifestErrorNotification </span> </td> 
   <td colname="2"> Det gick inte att hämta bakgrundsmanifestet. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerBufferingCompletedNotification </span> </td> 
   <td colname="2"> Buffring har slutförts. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerBufferingStartedNotification </span> </td> 
   <td colname="2"> Mediespelaren försätts i buffertläge. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTAudioTrackChangeCompleted </span> </td> 
   <td colname="2"> En ändring av ljudspåret för de media som spelas upp har slutförts. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTAudioTrackChangeStarted </span> </td> 
   <td colname="2"> En ändring av ljudspåret för det media som spelas upp initieras. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerItemChangedNotification </span> </td> 
   <td colname="2"> En annan <span class="codeph"> PTMediaPlayerItem </span> för <span class="codeph"> PTMediaPlayer </span> har angetts. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerItemDRMMetadataChanged </span> </td> 
   <td colname="2"> DRM-metadata har ändrats. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerMediaSelectionOptionsAvailableNotification </span> </td> 
   <td colname="2"> Det finns nya undertexter och alternativa ljudspår ( <span class="codeph"> PTMediaSelectionOption </span>). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerNewNotificationEntryAddedNotification </span> </td> 
   <td colname="2"> En ny <span class="codeph"> PTNotification </span> har lagts till i <span class="codeph"> PTNotificationHistoryItem </span> för den aktuella <span class="codeph"> </span>PTMediaPlayerItem, d.v.s. när en meddelandehändelse läggs till i meddelandehistoriken. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerPlayCompletedNotification </span> </td> 
   <td colname="2"> Medieuppspelningen har avslutats. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerSeekCompletedNotification </span> </td> 
   <td colname="2"> Sökningen har slutförts. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerSeekErrorNotification </span> </td> 
   <td colname="2"> Den aktuella sökåtgärden misslyckades. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerSeekStartedNotification </span> </td> 
   <td colname="2"> Sökningen startar. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerPlayStartedNotification </span> </td> 
   <td colname="2"> Uppspelningen har startats. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerStatusNotification </span> </td> 
   <td colname="2"> Spelarstatusen har ändrats. Möjliga statusvärden är: 
    <ul id="ul_DDBE8CAD5D5A46D2AAA6B98F0754A881"> 
     <li id="li_48F9AD580BCB4BB8A5C2DFED0DF9970F"> <p> <span class="codeph"> PTMediaPlayerStatusSkapad </span> </p> </li> 
     <li id="li_EDFB0765CF14422A95C9119DA3394163"> <p> <span class="codeph"> PTMediaPlayerStatusInitializing </span> </p> </li> 
     <li id="li_06E1576D50C646C19E88F0F14912F2C0"> <p> <span class="codeph"> PTMediaPlayerStatusInitialized </span> </p> </li> 
     <li id="li_E8B7157B5B234DFFABC2E5BEC241AB84"> <p> <span class="codeph"> PTMediaPlayerStatusReady </span> </p> </li> 
     <li id="li_FF2E66B390154EAA8791B4D874CC62E1"> <p> <span class="codeph"> PTMediaPlayerStatusSpela upp </span> </p> </li> 
     <li id="li_6F3306832B7642E4BEE84068383AFAF3"> <p> <span class="codeph"> PTMediaPlayerStatusPaused </span> </p> </li> 
     <li id="li_AE579AB888954F89A7F1115CAC0655E6"> <p> <span class="codeph"> PTMediaPlayerStatusStoppad </span> </p> </li> 
     <li id="li_A4CEB39374E84B4AA4F7202E67B9BE43"> <p> <span class="codeph"> PTMediaPlayerStatusSlutförd </span> </p> </li> 
     <li id="li_C50EB9C459264641A9FF70EF901D7474"> <p> <span class="codeph"> PTMediaPlayerStatusError </span> </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerTimeChangeNotification </span> </td> 
   <td colname="2"> Uppspelningens aktuella tid har ändrats. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerTimelineChangedNotification </span> </td> 
   <td colname="2"> Den aktuella spelarens tidslinje har ändrats. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" colsep="1" rowsep="1"> <span class="codeph"> PTTimedMetadataChangedNotification </span> </td> 
   <td colname="2"> TVSDK påträffade den första förekomsten av en prenumerationstagg. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTTimedMetadataChangedInBackgroundNotification </span> </td> 
   <td colname="2"> <p>En prenumerationstagg identifieras i bakgrundsmanifestet och en ny <span class="codeph"> PTTimedMetadata- </span> instans förbereds utifrån den. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Exempelhanterare för meddelanden {#section_D729C2403A234DD09596829D26882ADC}

Följande kodfragment illustrerar några av de sätt som du kan använda meddelanden på.

Hämta `PTAdBreak` instansen med `PTMediaPlayerAdBreakKey`:

```
 - (void) onMediaPlayerAdBreakStarted:(NSNotification *) notification { 
   // Fetch the PTAdBreak instance using PTMediaPlayerAdBreakKey 
   PTAdBreak *adBreak = [notification.userInfo objectForKey:PTMediaPlayerAdBreakKey]; 
   ... 
   ... 
} 
```

Ange `subtitlesOptions` och `audioOptions`:

```
 - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification \*) notification { 
   //SubtitlesOptions and audioOptions are set and accessible now. 
   NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions;  
   NSArray* audioOp tions = self.player.currentItem.audioOptions; 
   ... 
   ... 
} 
```

Hämta `PTAd` instansen med `PTMediaPlayerAdKey`:

```
 - (void) onMediaPlayerAdPlayStarted:(NSNotification \*)  notification { 
   // Fetch the PTAdinstance using PTMediaPlayerAdKey 
   PTAd *ad = [notification.userInfo objectForKey:PTMediaPlayerAdKey]; 
   ... 
   ... 
} 
```
