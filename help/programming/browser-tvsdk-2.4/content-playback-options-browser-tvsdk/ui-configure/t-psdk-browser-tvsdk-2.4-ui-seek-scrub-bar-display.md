---
description: I Browser TVSDK kan du söka till en viss position (tid) i en ström. En direktuppspelning kan vara en uppspelningslista med glidfönster eller VOD-innehåll (video on demand).
title: Hantera sökning när sökfältet används
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Hantera sökning när sökfältet används{#handle-seek-when-using-the-seek-bar}

I Browser TVSDK kan du söka till en viss position (tid) i en ström. En direktuppspelning kan vara en uppspelningslista med glidfönster eller VOD-innehåll (video on demand).

>[!IMPORTANT]
>
>Sökning i en liveström är endast tillåtet för DVR.

1. Vänta tills webbläsarens TVSDK är i ett giltigt söktillstånd.

   Giltiga lägen är PREPARED, COMPLETE, PAUSED och PLAYING. Om mediaresursen är i ett giltigt tillstånd kan du vara säker på att den har lästs in. Om spelaren inte är i ett giltigt sökbart läge kommer ett försök att anropa följande metoder att resultera i en `IllegalStateException`.

   Du kan till exempel vänta på att webbläsarens TVSDK ska utlösa  `AdobePSDK.MediaPlayerStatusChangeEvent`  med `event.status` av `AdobePSDK.MediaPlayerStatus.PREPARED`.

1. Skicka den begärda sökpositionen till `MediaPlayer.seek` som en parameter i millisekunder.

   Detta flyttar spelhuvudet till en annan position i strömmen.

   >[!TIP]
   >
   >Den begärda sökpositionen kanske inte sammanfaller med den faktiska beräknade positionen.

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. Vänta på att webbläsarens TVSDK ska aktivera  `AdobePSDK.PSDKEventType.SEEK_END`  som returnerar den justerade positionen i händelsens `actualPosition` attribute:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

   Detta är viktigt eftersom den faktiska startpositionen efter sökningen kan skilja sig från den begärda positionen. Vissa av följande regler kan gälla:

   * Uppspelningsbeteendet påverkas om en sökning, eller annan omplacering, slutar mitt i en annonsbrytning eller hoppar över annonsbrytningar.
   * Du kan bara söka efter resursens sökbara längd. För VOD är det från 0 till tillgångens varaktighet.

1. Avlyssna sökfältet som skapades i exemplet ovan `setPositionChangeListener()` för att se när användaren stegar igenom:

   ```js
   seekBar.setPositionChangeListener(function (pos) { 
                   var range = player.seekableRange; 
                   if (range) { 
                       var duration = range.duration; 
                       var time = duration * pos; // seek bar range is [0,1] 
                       player.seek(time); 
   
                       console.log("seek to " + time + " / " + duration); 
                   } 
   
               }); 
   ```

1. Konfigurera återanrop för händelseavlyssnare för ändringar i användarens sökaktivitet.

       Sökåtgärden är asynkron, så Browser TVSDK skickar dessa händelser som är relaterade till sökning:
   
   * `AdobePSDK.PSDKEventType.SEEK_BEGIN` för att ange att sökning påbörjas.
   * `AdobePSDK.PSDKEventType.SEEK_END` för att ange att sökningen lyckades.
   * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` för att ange att mediespelaren har justerat sökpositionen som anges av användaren.
