---
description: Du kan använda TimedMetadata när den aktuella uppspelningstiden matchar starttiden.
title: Använd tidsbestämda metadata
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Använd tidsbestämda metadata {#use-timed-metadata}

Du kan använda TimedMetadata när den aktuella uppspelningstiden matchar starttiden.

Använda dessa sparade `TimedMetadata` under uppspelning använder du de sparade `ArrayList` från [Lagra tidsbestämda metadataobjekt när de skickas](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md).

1. Kör en timer och fråga den aktuella uppspelningstiden upprepade gånger.
1. Hitta alla `TimedMetadata` objekt med starttider som matchar den aktuella uppspelningstiden.

   Du kan använda dessa objekt för att slutföra olika åtgärder.

   >[!IMPORTANT]
   >
   >Vid kontroll av om den aktuella uppspelningstiden matchar någon `TimedMetadata` objekt, inkludera `shouldTriggerSubscribedTagEvent` som ett villkor.

   Tidslinjen kan ändras på grund av olika annonsbeteenden. En eller flera annonsbrytningar kan till exempel flyttas från sina ursprungliga positioner på tidslinjen, men `shouldTriggerSubscribedTagEvent` säkerställer att `TimeMetadata` objektets starttid matchar den aktuella uppspelningstiden.

   Till exempel:

   ```java
    _playbackClockEventListener = new Clock.ClockEventListener() {
       @Override
       public void onTick(String name) {
           getActivity().runOnUiThread(new Runnable() {
               @Override
               public void run() {
                   /* handle timedmetadata object list  */ 
                   if (_mediaPlayer != null && _timedMetadataList != null && _timedMetadataList.size() > 0) {
                       if (_lastKnownStatus == MediaPlayer.PlayerState.PLAYING) {
                           long localTime = _mediaPlayer.getLocalTime();
                           Iterator<TimedMetadata> iterator = _timedMetadataList.iterator(); 
                           while (iterator.hasNext()) {
                               TimedMetadata timedMetadata = iterator.next();
                               long diff = localTime - timedMetadata.getTime();
                               if (diff >= 0 &&
                                   diff <= PLAYBACK_CLOCK_INTERVAL &&
                                   _mediaPlayer.shouldTriggerSubscribedTagEvent()) {
                                   // use timed metadata object
                               }
                           }
                       }
                   }
               }
           });
       }
   };
   _playbackClock.addClockEventListener(_playbackClockEventListener);
   ```

1. Justera streck regelbundet `TimedMetadata` -instanser i listan för att förhindra att minnet växer kontinuerligt.
