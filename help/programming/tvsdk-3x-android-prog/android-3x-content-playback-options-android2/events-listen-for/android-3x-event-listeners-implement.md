---
description: Med händelsehanterare kan du svara på TVSDK-händelser.
title: Implementera händelseavlyssnare och återanrop
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Implementera händelseavlyssnare och återanrop  {#implement-event-listeners-and-callbacks}

Med händelsehanterare kan du svara på TVSDK-händelser.

När en händelse inträffar anropar TVSDK:s händelsemekanism din registrerade händelsehanterare och skickar händelseinformationen.

TVSDK definierar avlyssnare som offentliga interna gränssnitt inuti `MediaPlayer` gränssnitt.

Programmet måste implementera händelseavlyssnare för alla TVSDK-händelser som påverkar programmet.

1. Avgör vilka händelser programmet ska lyssna efter.

   * Obligatoriska händelser: Lyssna efter alla uppspelningshändelser.

     >[!IMPORTANT]
     >
     >Lyssna efter statusförändringshändelsen, som inträffar när spelarens status ändras på sätt som du behöver veta. Informationen innehåller fel som kan påverka vad spelaren kan göra härnäst.

   * För andra händelser, beroende på ditt program, se  [Sammanfattning av händelser för Primetime Player](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md).

1. Implementera och lägg till en händelseavlyssnare för varje händelse.

   För de flesta händelser skickar TVSDK argument till händelseavlyssnarna. Sådana värden ger information om händelsen som kan hjälpa dig att bestämma vad du ska göra härnäst. The `MediaPlayerEvent` uppräkningen listar alla händelser som `MediaPlayer` skickar. Mer information finns i  [Sammanfattning av händelser för Primetime Player](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md).

   Om `mPlayer` är en instans av `MediaPlayer`, så här kan du lägga till och strukturera en händelseavlyssnare:

   ```java
   mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED, new StatusChangeEventListener() { 
       @Override 
       public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
           event.getMetadata(); 
           if (event.getMetadata() != null) {/* Do something */} 
           if (event.getStatus() == MediaPlayerStatus.IDLE) {/* Do something */} 
           else if (event.getStatus() == MediaPlayerStatus.INITIALIZED) {/* Do something */} 
           else if (event.getStatus() == MediaPlayerStatus.PREPARED) {/* Do something */} 
       } 
   }); 
   ```

## Ordning för uppspelningshändelser {#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK skickar händelser/meddelanden i vanligtvis förväntade sekvenser. Spelaren kan implementera åtgärder baserat på händelser i den förväntade sekvensen.

I följande exempel visas ordningen för vissa händelser som inträffar under uppspelningen.

När en medieresurs läses in `MediaPlayer.replaceCurrentResource`, är händelseordningen:

1. `MediaPlayerEvent.STATUS_CHANGED` med status `MediaPlayerStatus.INITIALIZING`

1. `MediaPlayerEvent.STATUS_CHANGED` med status `MediaPlayerStatus.INITIALIZED`

>[!TIP]
>
>Läs in din medieresurs på huvudtråden. Om du läser in en medieresurs i en bakgrundstråd kan den här åtgärden eller efterföljande åtgärder utlösa ett fel, t.ex. `MediaPlayerException`och avsluta.

När du förbereder för uppspelning genom `MediaPlayer.prepareToPlay`, är händelseordningen:

1. `MediaPlayerEvent.STATUS_CHANGED` med status `MediaPlayerStatus.PREPARING`

1. `MediaPlayerEvent.TIMELINE_UPDATED` om annonser infogades.
1. `MediaPlayerEvent.STATUS_CHANGED` med status `MediaPlayerStatus.PREPARED`

För live-/linjära strömmar, under uppspelningen när uppspelningsfönstret går framåt och ytterligare möjligheter är lösta, är händelseordningen:

1. `MediaPlayerEvent.ITEM_UPDATED`
1. `MediaPlayerEvent.TIMELINE_UPDATED` om annonser har infogats

## Ordning på reklamevenemang {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

När din uppspelning inkluderar annonsering skickar TVSDK händelser/meddelanden i de sekvenser som förväntas. Spelaren kan implementera åtgärder baserat på händelser i den förväntade sekvensen.

När annonser spelas upp är händelseordningen:

* `MediaPlayerEvent.AD_RESOLUTION_COMPLETE`

Följande händelser skickas för varje annons inom annonsbrytningen:

* `MediaPlayerEvent.AD_BREAK_START`
* `MediaPlayerEvent.AD_START`
* `MediaPlayerEvent.AD_PROGRESS (multiple times)`
* `MediaPlayerEvent.AD_CLICK (for each click)`
* `MediaPlayerEvent.AD_COMPLETE`
* `MediaPlayerEvent.AD_BREAK_COMPLETE`

I följande exempel visas ett typiskt förlopp för annonsuppspelningshändelser:

```
mediaPlayer.addEventListener(MediaPlayerEvent.AD_RESOLUTION_COMPLETE, new AdResolutionCompleteEventListener() { 
        @Override 
        public void onAdResolutionComplete() { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_BREAK_START, new AdBreakStartedEventListener() { 
         @Override 
        public void onAdBreakStarted(AdBreakPlaybackEvent adBreakPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_START, new AdStartedEventListener() { 
         @Override 
        public void onAdStarted(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_PROGRESS, new AdProgressEventListener() { 
         @Override 
         public void onAdProgress(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_COMPLETE, new AdCompletedEventListener() { 
         @Override 
         public void onAdCompleted(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_BREAK_COMPLETE, new AdBreakCompletedEventListener() { 
         @Override 
         public void onAdBreakCompleted(AdBreakPlaybackEvent adBreakPlaybackEvent) { ... } 
    }); 
 
Below event is for tracking ad clicks. 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_CLICK, new AdClickedEventListener() { 
         @Override 
         public void onAdClicked(AdClickEvent adClickEvent) { ... } 
    });
```

## Ordning för DRM-händelser {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK skickar DRM-händelser (Digital Rights Management) som svar på DRM-relaterade åtgärder som när nya DRM-metadata blir tillgängliga. Spelaren kan implementera åtgärder som svar på dessa händelser.

Om du vill få meddelanden om alla DRM-relaterade händelser avlyssnar du `MediaPlayerEvent.DRM_METADATA`. TVSDK skickar ytterligare DRM-händelser via `DRMManager` klassen.

## Ordning för inläsarhändelser {#section_5638F8EDACCE422A9425187484D39DCC}

TVSDK-utskick `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` när inläsarhändelser inträffar.
