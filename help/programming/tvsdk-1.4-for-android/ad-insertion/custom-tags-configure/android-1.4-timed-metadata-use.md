---
description: Du kan använda TimedMetadata när den aktuella uppspelningstiden matchar starttiden.
seo-description: Du kan använda TimedMetadata när den aktuella uppspelningstiden matchar starttiden.
seo-title: Använd tidsbestämda metadata
title: Använd tidsbestämda metadata
uuid: 98bb8c08-2794-42d6-b5c3-b1047ac804fe
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 1%

---


# Använd tidsbestämda metadata {#use-timed-metadata}

Du kan använda TimedMetadata när den aktuella uppspelningstiden matchar starttiden.

Om du vill använda de här sparade `TimedMetadata`-objekten under uppspelningen använder du de sparade `ArrayList` från [Lagra tidsbestämda metadataobjekt när de skickas](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md).

1. Kör en timer och fråga den aktuella uppspelningstiden upprepade gånger.
1. Hitta alla `TimedMetadata`-objekt med starttider som matchar den aktuella uppspelningstiden.

   Du kan använda dessa objekt för att slutföra olika åtgärder.

   >[!IMPORTANT]
   >
   >När du kontrollerar om den aktuella uppspelningstiden matchar några `TimedMetadata`-objekt ska du ta med `shouldTriggerSubscribedTagEvent` som villkor.

   Tidslinjen kan ändras på grund av olika annonsbeteenden. En eller flera annonsbrytningar kan till exempel flyttas från sina ursprungliga positioner på tidslinjen, men med `shouldTriggerSubscribedTagEvent` säkerställer du att starttiden för `TimeMetadata`-objektet matchar den aktuella uppspelningstiden.

   Exempel:

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

1. Justera regelbundet inaktuella `TimedMetadata`-instanser från listan för att förhindra att minnet växer kontinuerligt.