---
description: I Browser TVSDK kan du söka till en viss position (tid) i en ström. En direktuppspelning kan vara en uppspelningslista med glidfönster eller VOD-innehåll (video on demand).
seo-description: I Browser TVSDK kan du söka till en viss position (tid) i en ström. En direktuppspelning kan vara en uppspelningslista med glidfönster eller VOD-innehåll (video on demand).
seo-title: Hantera sökning när sökfältet används
title: Hantera sökning när sökfältet används
uuid: a7c74141-581f-40a3-9d28-ce56ba56773c
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Hantera sökning när sökfältet används{#handle-seek-when-using-the-seek-bar}

I Browser TVSDK kan du söka till en viss position (tid) i en ström. En direktuppspelning kan vara en uppspelningslista med glidfönster eller VOD-innehåll (video on demand).

>[!IMPORTANT]
>
>Sökning i en liveström är endast tillåtet för DVR.

1. Vänta tills webbläsarens TVSDK är i ett giltigt söktillstånd.

   Giltiga lägen är PREPARED, COMPLETE, PAUSED och PLAYING. Om mediaresursen är i ett giltigt tillstånd kan du vara säker på att den har lästs in. Om spelaren inte är i ett giltigt sökbart läge genereras ett `IllegalStateException`fel om du försöker anropa följande metoder.

   Du kan till exempel vänta på att webbläsarens TVSDK ska utlösas `AdobePSDK.MediaPlayerStatusChangeEvent` med ett `event.status` av `AdobePSDK.MediaPlayerStatus.PREPARED`.

1. Skicka den begärda sökpositionen till `MediaPlayer.seek` metoden som en parameter i millisekunder.

   Detta flyttar spelhuvudet till en annan position i strömmen.

   >[!TIP]
   >
   >Den begärda sökpositionen kanske inte sammanfaller med den faktiska beräknade positionen.

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. Vänta tills Browser TVSDK utlöser `AdobePSDK.PSDKEventType.SEEK_END` händelsen, som returnerar den justerade positionen i händelsens `actualPosition` attribut:

       &quot;js
     player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete);
       onSeekComplete = function (event) {
     // event.actualPosition
     }
     &quot;
     
     Detta är viktigt eftersom den faktiska startpositionen efter sökningen kan skilja sig från den begärda positionen. Vissa av följande regler kan gälla:
   
   * Uppspelningsbeteendet påverkas om en sökning, eller annan omplacering, slutar mitt i en annonsbrytning eller hoppar över annonsbrytningar.
   * Du kan bara söka efter resursens sökbara längd. För VOD är det från 0 till tillgångens varaktighet.

1. Avlyssna sökfältet som skapades i exemplet ovan för `setPositionChangeListener()` att se när användaren stegar igenom:

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

