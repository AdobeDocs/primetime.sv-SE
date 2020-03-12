---
description: Textning för hörselskadade visar ljudet i en video som text på skärmen när ljudet inte kan höras eller när tittaren inte hörs.
seo-description: Textning för hörselskadade visar ljudet i en video som text på skärmen när ljudet inte kan höras eller när tittaren inte hörs.
seo-title: Välj ett aktuellt bildtextspår bland tillgängliga spår
title: Välj ett aktuellt bildtextspår bland tillgängliga spår
uuid: 637a70c9-9bef-4b13-8b1f-62f22f983e80
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Välj ett aktuellt bildtextspår bland tillgängliga spår{#select-a-current-caption-track-from-among-available-tracks}

Du kan välja ett spår i en lista med tillgängliga textningsspår. Detta blir det aktuella spåret, som visas när synligheten är aktiverad. Vissa spår kanske inte är tillgängliga från början, så lyssna efter händelsen som anger att fler har blivit tillgängliga.

>[!TIP]
>
>Undertexter är alltid aktiverade. Alla standardspår för undertextning anses finnas. Standardspår (som CC1-CC4, CS1-CS6) räknas upp i `ClosedCaptionsTrack.DefaultCCTypes`. När uppspelningen börjar letar TVSDK efter aktivitet i någon av dessa kanaler. Om den hittar aktivitet, anger den metoden för det spåret och skickar `isActive` `MediaPlayer.PlaybackEventListener.onUpdated` händelsen.

1. Vänta tills mediespelaren är i åtminstone tillståndet PREPARED.
1. Lyssna efter dessa händelser:

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: Den första listan med spår för undertextning är tillgänglig

1. Hämta en lista över alla tillgängliga undertextningsspår.

   Exempel:

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
         mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. Välj ett tillgängligt spår som aktuellt spår.

   Exempel:

   ```java
   // Select the initial CC track. 
   for (int i = 0; i < ccTracks.size(); i++) { 
       ClosedCaptionsTrack track = ccTracks.get(i); 
       if (track.getName().equals(INITIAL_CC_TRACK)) { 
   
<b>mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track);</b>
selectedClosedCaptionsIndex = i;
}}

```
1. Implement a listener for the event that indicates that more tracks are available. When TVSDK dispatches the event, retrieve the current list of available tracks.

Retrieve the list each time that the event occurs to ensure that you always have the most current list.

