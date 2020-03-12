---
description: Händelsehanterare gör att TVSDK kan svara på händelser.
seo-description: Händelsehanterare gör att TVSDK kan svara på händelser.
seo-title: Implementera händelseavlyssnare och återanrop
title: Implementera händelseavlyssnare och återanrop
uuid: 6b7859a4-55f9-48b1-b1f1-7b79bc92610a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Implementera händelseavlyssnare och återanrop{#implement-event-listeners-and-callbacks}

Händelsehanterare gör att TVSDK kan svara på händelser.

När en händelse inträffar anropar TVSDK:s händelsemekanism din registrerade händelsehanterare och skickar händelseinformationen till hanteraren.

TVSDK definierar avlyssnare som offentliga interna gränssnitt i `MediaPlayer` gränssnittet.

Ditt program måste implementera händelseavlyssnare för TVSDK-händelser som påverkar ditt program.

En fullständig lista över händelser för videoanalys finns i Spåra grundläggande videouppspelning.

1. Avgör för vilka händelser ditt program måste avlyssna.

   * **Nödvändiga händelser**: Lyssna efter alla uppspelningshändelser.

      >[!IMPORTANT]
      >
      >Uppspelningshändelsen `onStateChanged` anger spelarens tillstånd, inklusive fel. Alla lägen kan påverka spelarens nästa steg

   * **Andra händelser**: Valfritt, beroende på ditt program.

      Om du till exempel inkluderar annonsering i uppspelningen implementerar du AdPlaybackEventListener-återanropen.

1. Implementera händelseavlyssnare för varje händelse.

   TVSDK returnerar parametervärden till återanrop till händelseavlyssnaren. Dessa värden ger relevant information om händelsen som du kan använda i dina avlyssnare för att utföra lämpliga åtgärder.

   `MediaPlayer.EventListener` visar alla gränssnitt för återanrop. Varje gränssnitt visar det återanropsnamn och de parametrar som returneras för varje händelse.

   Exempel:

   ```
   MediaPlayer.PlaybackEventListener.onStateChanged( 
    MediaPlayer.PlayerState state, MediaPlayerNotification notification)
   ```

1. Registrera dina callback-avlyssnare hos `MediaPlayer` objektet med hjälp av `MediaPlayer.addEventListener`.

   ```
   mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, 
    new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onStateChanged( 
    MediaPlayer.PlayerState state, 
    MediaPlayerNotification notification) {...} 
   }
   ```

## Ordning för uppspelningshändelser {#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK skickar händelser/meddelanden i vanligtvis förväntade sekvenser. Spelaren kan implementera åtgärder baserat på händelser i den förväntade sekvensen.

I följande exempel visas ordningen för vissa händelser som innehåller uppspelningshändelser.

* När en medieresurs läses in via `MediaPlayer.replaceCurrentResource`är händelseordningen:

1. `MediaPlayer.PlaybackEventListener.onStateChanged` med läge `MediaPlayer.PlayerState.INITIALIZING`

1. `MediaPlayer.PlaybackEventListener.onStateChanged` med läge `MediaPlayer.PlayerState.INITIALIZED`

>[!TIP]
>
>Läs in din medieresurs på huvudtråden. Om du läser in en medieresurs på en bakgrundstråd kan den här åtgärden eller efterföljande TVSDK-åtgärder, eller båda, generera ett fel (till exempel `IllegalStateException`) och avsluta.

* När du förbereder för uppspelning genom `MediaPlayer.prepareToPlay`är händelseordningen:

1. `MediaPlayer.PlaybackEventListener.onStateChanged` med läge `MediaPlayerStatus.PREPARING`

1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` om annonser infogades.
1. `MediaPlayer.PlaybackEventListener.onStateChanged` med läge `MediaPlayerStatus.PREPARED`

* För live-/linjära strömmar, under uppspelningen när uppspelningsfönstret går framåt och ytterligare möjligheter är lösta, är händelseordningen:

1. `MediaPlayer.PlaybackEventListener.onUpdated`
1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` om annonser har infogats
1. `MediaPlayerItemEvent.ITEM_UPDATED`
1. `TimelineEvent.TIMELINE_UPDATED` om annonser har infogats

I följande exempel visas ett typiskt händelseförlopp:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK,  
  new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() {...} 
    @Override 
    public void onUpdated() {...} 
    @Override 
    public void onPlayStart() {...} 
    @Override 
    public void onPlayComplete() {...} 
    @Override 
    public void onSizeAvailable(long height, long width) {...} 
    @Override 
    public void onStateChanged(MediaPlayer.PlayerState state,  
      MediaPlayerNotification notification) {...} 
});
```

## Ordning på annonsevenemang {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

När din uppspelning inkluderar annonsering skickar TVSDK händelser/meddelanden i de sekvenser som förväntas. Spelaren kan implementera åtgärder baserat på händelser i den förväntade sekvensen.

När annonser spelas upp är händelseordningen:

* `AdPlaybackEventListener.onAdBreakStart`
* Följande skickas för varje annons i annonsbrytningen:

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` (flera gånger under en annons uppspelning)
   * `AdPlaybackEventListener.onAdClick` (för varje klick)
   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdBreakComplete`

I följande exempel visas ett typiskt förlopp för annonsuppspelningshändelser:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.AD_PLAYBACK,  
  new MediaPlayer.AdPlaybackEventListener() { 
    @Override  
    public void onAdBreakStart(AdBreak adBreak) { ... } 
    @Override 
    public void onAdStart(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdProgress(AdBreak adBreak, Ad ad, int percentage) { ... }  
    @Override 
    public void onAdComplete(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdBreakComplete(AdBreak adBreak) { ... } 
    @Override 
    public void onAdClick(AdBreak adBreak, Ad ad, AdClick adClick) { ... } 
});
```

När annonser spelas upp är händelseordningen:

* `AdPlaybackEventListener.onAdBreakStart`
* Följande skickas för varje annons i annonsbrytningen:

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` (flera gånger under en annons uppspelning)
   * `AdPlaybackEventListener.onAdClick` (för varje klick)
   * `AdPlaybackEventListener.onAdStart`

* `AdPlaybackEventListener.onAdBreakComplete`

I följande exempel visas ett typiskt förlopp för annonsuppspelningshändelser:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.AD_PLAYBACK,  
  new MediaPlayer.AdPlaybackEventListener() { 
    @Override  
    public void onAdBreakStart(AdBreak adBreak) { ... } 
    @Override 
    public void onAdStart(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdProgress(AdBreak adBreak, Ad ad, int percentage) { ... }  
    @Override 
    public void onAdComplete(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdBreakComplete(AdBreak adBreak) { ... } 
    @Override 
    public void onAdClick(AdBreak adBreak, Ad ad, AdClick adClick) { ... } 
});
```

## QoS-händelser {#section_9BFF3CD7AA1C4BD6960ACF6B9C0B25CC}

TVSDK skickar QoS-händelser (Quality of Service) för att meddela programmet om händelser som kan påverka beräkningen av QoS-statistik, som buffring och sökning av händelser.

I följande exempel visas en typisk progression av dessa händelser:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.QOS,  
  new MediaPlayer.QOSEventListener(){ 
    //For buffering activity 
    @Override 
    public void onBufferStart() 
    @Override 
    public void onBufferComplete() 
    // For seeking 
    @Override 
    public void onSeekStart() 
    @Override 
    public void onSeekComplete(long adjustedTime) 
    @Override 
    public void onLoadComplete (MediaPlayerItem mediaplayeritem) 
    @Override 
    public void onLoadInfo(LoadInfo loadInfo) 
    @Override 
    public void onOperationFailed(MediaPlayerNotification.Warning warning) 
});
```

## DRM-händelser {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK skickar DRM-händelser (Digital Rights Management) som svar på DRM-relaterade åtgärder som när nya DRM-metadata blir tillgängliga. Spelaren kan implementera åtgärder som svar på dessa händelser.

Om du vill få meddelanden om alla DRM-relaterade händelser lyssnar du efter `onDRMMetadata(DRMMetadataInfo drmMetadataInfo)`. TVSDK skickar ytterligare DRM-händelser via `DRMManager` klassen.

I följande exempel visas ett typiskt förlopp:

```
mediaPlayer.addEventListener(MediaPlayer.Event.DRM, 
 new MediaPlayer.DRMEventListener() { 
 @Override 
 public void onDRMMetadata(byte[] data, int length, long timestamp) {...} 
}); 
```

## Loader-händelser {#section_5638F8EDACCE422A9425187484D39DCC}

Spelaren kan implementera åtgärder baserat på följande händelser:

| Händelse | Betydelse |
|---|---|
| `onLoadComplete (mediaPlayerItem playerItem)` | Inläsningen av medieresursen har slutförts. |
| `onError` | Ett problem uppstod vid inläsning av medieresurser. |

