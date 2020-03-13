---
description: När en användare klickar på en annons bör programmet pausa uppspelningen av huvudvideoinnehållet.
seo-description: När en användare klickar på en annons bör programmet pausa uppspelningen av huvudvideoinnehållet.
seo-title: Pausa och återuppta uppspelning
title: Pausa och återuppta uppspelning
uuid: 87ba9f05-912d-4b85-8add-feb26a796a3a
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Pausa och återuppta uppspelning {#pause-and-resume-playback}

När en användare klickar på en annons bör programmet pausa uppspelningen av huvudvideoinnehållet.

1. Åsidosätt `onPause` och `onResume` från Android-aktivitet.

   ```java
   @Override 
   public void onResume() { 
       super.onResume(); 
       requestAudioFocus(); 
       if (_lastKnownStatus == MediaPlayerStatus.PAUSED) { 
           _mediaPlayer.play(); 
       } 
   } 
   ... 
   
   @Override 
   public void onPause() { 
       super.onPause(); 
       if (_mediaPlayer != null) { 
           if (_mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING || 
             _mediaPlayer.getStatus() == MediaPlayerStatus.PAUSED) { 
               _savedPlayerStatus = _mediaPlayer.getStatus(); 
               _lastKnownTime = _mediaPlayer.getCurrentTime(); 
           } 
           if (_mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING) { 
               _mediaPlayer.pause(); 
               _lastKnownStatus = MediaPlayerStatus.PAUSED; 
           } 
       } 
   } 
   abandonAudioFocus(); 
   ```

