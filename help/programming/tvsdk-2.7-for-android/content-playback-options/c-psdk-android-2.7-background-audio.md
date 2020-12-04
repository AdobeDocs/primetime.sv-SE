---
seo-title: Aktivera bakgrundsljud
title: Aktivera bakgrundsljud
uuid: 1e7319f5-ee16-47bd-bfd5-d3dcfe69bf4b
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# Aktivera bakgrundsljud {#enable-background-audio}

Om du vill aktivera ljuduppspelning när programmet är i bakgrunden ska programmet anropa `enableAudioPlaybackInBackground` API för MediaPlayer med true som argument när spelaren är i läget PREPARED.

```
_mediaPlayer.enableAudioPlaybackInBackground(true);
```

Appen bör pausa uppspelningen när den tappar greppet om ljudfokus under händelser som att svara på telefonen osv. Följande kodfragment visar hur du implementerar `OnAudioFocusChangeListener`:

```
/** 
 * Register the AudioFocus Change listener to track Audio focus from device. 
 */ 
 AudioManager.OnAudioFocusChangeListener onAudioFocusChangeListener = new AudioManager.OnAudioFocusChangeListener(){ 
     @Override 
     public void onAudioFocusChange(int focusChange){ 
          switch(focusChange){ 
               case AudioManager.AUDIOFOCUS_GAIN: 
                    break; 
               case AudioManager.AUDIOFOCUS_LOSS_TRANSIENT_CAN_DUCK: 
                    /* lower output volume*/ 
                    break; 
               case AudioManager.AUDIOFOCUS_LOSS: 
               case AudioManager.AUDIOFOCUS_LOSS_TRANSIENT: 
                    if(_lastKnownStatus ==MediaPlayerStatus.PLAYING) 
                         _mediaPlayer.pause(); 
                    break; 
          } 
     } 
}; 
 
AudioManager audioManager = (AudioManager) getActivity().getApplicationContext().getSystemService(Context.AUDIO_SERVICE); 
audioManager.requestAudioFocus(onAudioFocusChangeListener, AudioManager.STREAM_MUSIC, AudioManager.AUDIOFOCUS_GAIN);
```

