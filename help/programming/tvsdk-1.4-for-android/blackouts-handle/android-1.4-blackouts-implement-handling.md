---
description: TVSDK tillhandahåller API:er och exempelkod för hantering av utbrottsperioder.
title: Implementera hantering av strömavbrott
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# Implementera hantering av strömavbrott{#implement-blackout-handling}

TVSDK tillhandahåller API:er och exempelkod för hantering av utbrottsperioder.

Så här implementerar du hantering av strömavbrott, inklusive att tillhandahålla alternativt innehåll under strömavbrott:

1. Konfigurera appen för att identifiera svarta out-taggar i ett liveströmsmanifest.

   ```java
   public void createMediaPlayer { 
       ... 
       String[] blackoutTags = {BLACKOUTTAG}; 
       PSDKConfig.setSubscribedTags(blackoutTags); 
       // For example: PTSDKConfig.setSubscribedTags({"#EXT-OATCLS-SCTE35"}); 
   }
   ```

1. Skapa händelseavlyssnare för tidsbestämda metadatahändelser i förgrunds- och bakgrundsströmmar.

   ```java
   private MediaPlayer createMediaPlayer() { 
       mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, _playbackEventListener); 
       mediaPlayer.addEventListener(MediaPlayer.Event.BLACKOUTS, _blackoutsEventListener); 
   }
   ```

1. Implementera händelsehanterare för tidsbestämda metadata för både förgrunds- och bakgrundsströmmar.

   Förgrund:

   ```java
   private final MediaPlayer.PlaybackEventListener _playbackEventListener =  
             new MediaPlayer.PlaybackEventListener() { 
       ... 
   
       @override 
       public void onTimedMetadata(TimedMetadata timedMetadata) { 
           if (timedMetadata.getName().equal(BLACKOUTTAG) &&  
               !_timedMetadataList.contains(timedMetadata)) { 
                 _timedMetadataList.add(timedMetadata); 
           } 
       } 
       ... 
   } 
   
   private final MediaPlayer.BlackoutsEventListener _blackoutsEventListener =  
     new MediaPlayer.BlackoutsEventListener() { 
       @Override 
       public void onTimedMetadataInBackgroundItem(TimedMetadata timedMetadata) { 
           TimedMetadata.Type type = timedMetadata.getType(); 
           if (type.equals(TimedMetadata.Type.TAG) && _mediaPlayer.getPlaybackRange() != null  
               && _mediaPlayer.getPlaybackRange().getDuration() > 0) { 
               if (!_timedMetadataList.contains(timedMetadata) && isBlackoutMetadata(timedMetadata)) { 
                   _timedMetadataList.add(timedMetadata); 
               } 
           } 
       } 
   
       @Override 
       public void onBackgroundManifestFailed() { 
           ... 
       } 
   }; 
   ```

1. Handtag `TimedMetadata` objekt när `MediaPlayer` tiden går.

   ```java
   _playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           getActivity().runOnUiThread(new Runnable() { 
               @Override 
               public void run() { 
                   /* handle timedmetadata object list  */ 
                   if (_mediaPlayer != null && _timedMetadataList != null  
                       && _timedMetadataList.size() > 0) { 
                       if (_lastKnownStatus == MediaPlayer.PlayerState.PLAYING) { 
                           long localTime = _mediaPlayer.getLocalTime(); 
                           handleTimedMetadataList(localTime);      
                       } 
                   } 
               }                        
           }); 
       } 
   };
   ```

1. Skapa metoder för att växla innehåll i början och slutet av den svarta punkten.

   ```java
   private void handleTimedMetadataList(long currentTime) { 
       for (int i = 0; i < _timedMetadataList.size(); i++) { 
           TimedMetadata timedMetadata = _timedMetadataList.get(i); 
           long diff = localTime - timedMetadata.getTime(); 
           if (!_timedMetadataDispatchedList.contains(timedMetadata) 
               && diff >= 0 
               && diff <= PLAYBACK_CLOCK_INTERVAL 
               && _mediaPlayer.shouldTriggerSubscribedTagEvent()) { 
                   // switch to blackout content 
               if (!_inBlackout && isBlackoutStartTimedMetadata(timedMetadata)) { 
                   MediaResource blackoutMediaResource = createBlackoutMediaResource(timedMetadata); 
   
                   //1. register current item as background item 
                   _mediaPlayer.registerCurrentItemAsBackgroundItem(); 
   
                   //2. replace current item with blackout item 
                   _mediaPlayer.replaceCurrentItem(blackoutMediaResource); 
   
                   //3. update qos metrics 
                   _mediaQosProvider.updateMetrics(_mediaPlayer); 
   
                   //4. maintain state 
                   _inBlackout = true; 
                   resetTimedMetada(); 
   
                   break; 
               } 
               // switch back to main content 
               else if (_inBlackout && isBlackoutEndTimedMetadata(timedMetadata)) { 
                   //1. register current item as background item 
                   _mediaPlayer.unregisterCurrentBackgroundItem(); 
   
                   //2. replace current item with blackout item 
                   _mediaPlayer.replaceCurrentItem(_oldMediaResource); 
   
                   //3. update qos metrics 
                   _mediaQosProvider.updateMetrics(_mediaPlayer); 
   
                   //4. maintain state 
                   _inBlackout = false; 
                   resetTimedMetada(); 
   
                   break; 
               } 
           } 
       } 
   }
   ```

1. Uppdatera icke sökbara intervall om det svarta området finns i DVR i uppspelningsströmmen.

   ```java
   // prepare and update blackout nonSeekable ranges 
   
   List<TimeRange> blackoutRanges = prepareBlackoutRanges(_timedMetadataList); 
   if (blackoutRanges != null && blackoutRanges.size() > 0) { 
       int size = blackoutRanges.size(); 
       TimeRange[] blackoutRangesArray = blackoutRanges.toArray(new TimeRange[size]); 
       BlackoutMetadata blackoutMetadata = new BlackoutMetadata(blackoutRangesArray); 
       updateBlackoutMetadata(blackoutMetadata); 
   } 
   
   // function to update blackout metadata 
   private void updateBlackoutMetadata(BlackoutMetadata blackoutMetadata) { 
       MediaPlayerItem currentItem = _mediaPlayer.getCurrentItem(); 
       if (currentItem != null) { 
           Metadata metadata = currentItem.getResource().getMetadata(); 
           if (metadata != null) { 
               MetadataNode metadataNode = ((MetadataNode) metadata); 
               metadataNode.setNode(DefaultMetadataKeys.BLACKOUT_METADATA_KEY.getValue(),  
                                    blackoutMetadata); 
   
               for (int i = 0; i < blackoutMetadata.getNonSeekableRanges().length; i++) { 
                   TimeRange timeRange = blackoutMetadata.getNonSeekableRanges()[i]; 
               } 
           } 
       } 
   }
   ```

   >[!NOTE]
   >
   >För flera liveströmmar med bithastighet kan de justerbara bithastighetsprofilerna (ABR) ibland bli osynkroniserade. Detta orsakar en dubblett `timedMetadata` objekt för samma prenumerationstagg. För att undvika felaktiga beräkningar som inte går att söka efter bör du kontrollera om det finns överlappande icke sökbara intervall efter dina beräkningar, som i följande exempel:

   ```java
   List<TimeRange> rangesToRemove = new ArrayList<TimeRange>(); 
   
   for (int i = 0; i < nonSeekableRanges.size() - 1; i++) { 
       TimeRange range1 = nonSeekableRanges.get(i); 
       TimeRange range2 = nonSeekableRanges.get(i + 1); 
       if (range1.contains(range2.getBegin()) && !rangesToRemove.contains(range2)) { 
          rangesToRemove.add(range2); 
       } else if (range2.contains(range1.getBegin()) && !rangesToRemove.contains(range1)) { 
          rangesToRemove.add(range1); 
      } 
   } 
   
   if (nonSeekableRanges.size() > 0 && rangesToRemove.size() > 0) { 
       nonSeekableRanges.removeAll(rangesToRemove); 
       for (int i = 0; i < rangesToRemove.size(); i++) { 
           TimeRange range = rangesToRemove.get(i); 
       } 
   } 
   
   if (nonSeekableRanges.size() > 0 && rangesToRemove.size() > 0) { 
       nonSeekableRanges.removeAll(rangesToRemove); 
   }
   ```
