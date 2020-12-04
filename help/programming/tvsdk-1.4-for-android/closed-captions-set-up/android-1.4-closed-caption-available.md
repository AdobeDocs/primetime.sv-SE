---
description: Textning för hörselskadade visar ljudet i en video som text på skärmen när ljudet inte kan höras eller när tittaren inte hörs.
seo-description: Textning för hörselskadade visar ljudet i en video som text på skärmen när ljudet inte kan höras eller när tittaren inte hörs.
seo-title: Välj ett aktuellt bildtextspår bland tillgängliga spår
title: Välj ett aktuellt bildtextspår bland tillgängliga spår
uuid: 637a70c9-9bef-4b13-8b1f-62f22f983e80
translation-type: tm+mt
source-git-commit: 53924aa8ba90555d58d15ee10fb14221c7dffaff
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---


# Välj ett aktuellt bildtextspår bland tillgängliga spår{#select-a-current-caption-track-from-among-available-tracks}

Du kan välja ett spår i en lista med tillgängliga textningsspår. Detta blir det aktuella spåret, som visas när synligheten är aktiverad. Vissa spår kanske inte är tillgängliga från början, så lyssna efter händelsen som anger att fler har blivit tillgängliga.

>[!TIP]
>
>Undertexter är alltid aktiverade. Alla standardspår för undertextning anses finnas. Standardspår (som CC1-CC4, CS1-CS6) räknas upp i `ClosedCaptionsTrack.DefaultCCTypes`. När uppspelningen börjar letar TVSDK efter aktivitet i någon av dessa kanaler. Om den hittar aktivitet anges metoden `isActive` för det spåret och händelsen `MediaPlayer.PlaybackEventListener.onUpdated` skickas.

1. Vänta tills mediespelaren är i åtminstone tillståndet PREPARED.
1. Lyssna efter dessa händelser:

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: Den första listan med spår för undertextning är tillgänglig

1. Hämta en lista med alla tillgängliga undertextningsspår.

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
           mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track); 
           selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. Implementera en avlyssnare för händelsen som anger att fler spår är tillgängliga. När TVSDK skickar händelsen hämtar du den aktuella listan med tillgängliga spår.

   Hämta listan varje gång händelsen inträffar för att se till att du alltid har den senaste listan.
