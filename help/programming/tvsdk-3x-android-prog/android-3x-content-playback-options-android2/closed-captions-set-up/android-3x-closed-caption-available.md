---
description: Du kan välja ett spår i en lista med tillgängliga textningsspår. Detta blir det aktuella spåret, som visas när synligheten är aktiverad. Vissa spår kanske inte är tillgängliga från början, så lyssna efter händelsen som anger att fler har blivit tillgängliga.
title: Välj ett aktuellt bildtextspår bland tillgängliga spår
exl-id: 9f1a0f7e-44f8-4595-8879-568ab237ca1c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Välj ett aktuellt bildtextspår bland tillgängliga spår {#select-a-current-caption-track-from-among-available-tracks}

Du kan välja ett spår i en lista med tillgängliga textningsspår. Detta blir det aktuella spåret, som visas när synligheten är aktiverad. Vissa spår kanske inte är tillgängliga från början, så lyssna efter händelsen som anger att fler har blivit tillgängliga.

1. Vänta tills mediespelaren är i åtminstone `PREPARED` status.
1. Lyssna efter dessa händelser:

   * `MediaPlayerEvent.STATUS_CHANGED` med status `MediaPlayerStatus.INITIALIZED`: Den inledande listan med spår för undertextning är tillgänglig.

1. Hämta en lista med alla tillgängliga undertextningsspår.

   Till exempel:

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
     mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. Välj ett tillgängligt spår som aktuellt spår.

   Till exempel:

   ```java
   // Select the initial CC track. 
   for (int i = 0; i < ccTracks.size(); i++) { 
       ClosedCaptionsTrack track = ccTracks.get(i); 
       if (track.getName().equals(INITIAL_CC_TRACK)) {
        <b>mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track);</b> 
             selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. Implementera en avlyssnare för händelsen som anger att fler spår är tillgängliga. När TVSDK skickar händelsen hämtar du den aktuella listan med tillgängliga spår.

   Hämta listan varje gång händelsen inträffar för att se till att du alltid har den senaste listan.
