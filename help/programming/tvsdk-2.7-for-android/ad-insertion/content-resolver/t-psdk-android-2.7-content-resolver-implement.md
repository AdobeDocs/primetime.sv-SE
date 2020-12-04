---
description: Du kan implementera egna innehållslösningar baserat på standardlösare.
seo-description: Du kan implementera egna innehållslösningar baserat på standardlösare.
seo-title: Implementera en anpassad innehållshanterare
title: Implementera en anpassad innehållshanterare
uuid: bc0eda17-9b5d-4733-8e93-790758e68df5
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 2%

---


# Implementera en anpassad innehållshanterare {#implement-a-custom-content-resolver}

Du kan implementera egna innehållslösningar baserat på standardlösare.

När TVSDK genererar en ny affärsmöjlighet itererar företaget genom de registrerade innehållsmatcharna och letar efter en som kan lösa den affärsmöjligheten. Den första som returnerar `true` markeras för att lösa affärsmöjligheten. Om ingen innehållslösare kan användas hoppas den möjligheten över. Eftersom innehållsmatchningsprocessen vanligtvis är asynkron ansvarar innehållslösaren för att meddela TVSDK när processen har slutförts.

1. Implementera din egen anpassade `ContentFactory` genom att utöka gränssnittet `ContentFactory` och åsidosätta `retrieveResolvers`.

   Exempel:

   ```java
   class MyContentFactory extends ContentFactory { 
       @Override 
       public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { 
           List<ContentResolver> resolvers = new ArrayList<ContentResolver>(); 
           MediaPlayerItemConfig itemConfig = item.getConfig(); 
           if(itemConfig) { 
               CustomRangeMetadata customRanges = itemConfig.getCustomRangeMetadata(); 
               if (customRanges) { 
                   List<ReplaceTimeRange> timeRanges = customRanges.getTimeRangeList(); 
   
                   if (timeRanges && timeRanges.size() > 0) 
                   { 
                   // CustomRangeResolver is only activated by the presence of CustomRanges in configuration 
                   resolvers.add(new CustomRangeResolver()); 
                   } 
               } 
               AdvertisingMetadata metadata = itemConfig.getAdvertisingMetadata(); 
               if (metadata) { 
                   if (metadata instanceOf AuditudeSettings)  
                       resolvers.add(new AuditudeResolver(getContext());    
                   } 
               } 
           // add your custom resolver if any 
           resolvers.add(MyOpportunityGenerator(item)); 
           return resolvers; 
       } 
       ... 
   } 
   ```

1. Registrera `ContentFactory` till `MediaPlayer`.

   Exempel:

   ```java
   //Register the custom content factory with the media player 
   MediaPlayerItemConfig config = new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new MyContentFactory()); 
   
   //Pass this config while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config); 
   
   // OR use MediaPlayerItemLoader to pre-load a resource 
   id = 23; 
   itemLoader.load(resource, id, config);
   ```

1. Skicka ett `AdvertisingMetadata`-objekt till TVSDK enligt följande:
   1. Skapa ett `AdvertisingMetadata`-objekt.
   1. Spara `AdvertisingMetadata`-objektet till `MediaPlayerItemConfig`.

      ```java
      AdvertisingMetadata advertisingMetadata = new AdvertisingMetadata(); 
      
      advertisingMetadata.setDelayAdLoading(true); 
      ... 
      
      mediaPlayerItemConfig.setAdvertisingMetadata(advertisingMetadata); 
      ```

1. Skapa en anpassad annonsupplösarklass som utökar klassen `ContentResolver`.
   1. I den anpassade annonslösaren åsidosätter du `doConfigure`, `doCanResolve`, `doResolve`, `doCleanup`:

      ```java
      void doConfigure(MediaPlayerItem item); 
      boolean doCanResolve(Opportunity opportunity); 
      void doResolve(Opportunity opportunity); 
      void doCleanup();
      ```

      Du kan hämta din `advertisingMetadata` från objektet som skickades i `doConfigure`:

      ```java
      MediaPlayerItemConfig itemConfig = item.getConfig(); 
      
      AdvertisingMetadata advertisingMetadata =  
        mediaPlayerItemConfig.getAdvertisingMetadata(); 
      ```

   1. Skapa en `List<TimelineOperation>` för varje placeringsmöjlighet.

      Det här exemplet `TimelineOperation` innehåller en struktur för `AdBreakPlacement`:

      ```java
      AdBreakPlacement( 
          new AdBreak( ads,    // Vector<Ad> 
                       tracker // Content Tracker 
          ), 
          placementInformation // Retrieved from Opportunity 
      ); 
      ```

   1. När annonserna är lösta anropar du någon av följande funktioner:

      * Om annonsen lyckas ringer du `process(List<TimelineOperation> proposals)` och `notifyCompleted(Opportunity opportunity)` på `ContentResolverClient`

         ```java
         _client.process(timelineOperations); 
         _client.notifyCompleted(opportunity); 
         ```

      * Om annonsupplösningen misslyckas ringer du `notifyResolveError` på `ContentResolverClient`

         ```java
         _client.notifyFailed(Opportunity opportunity, PSDKErrorCode error);
         ```

         Exempel:

         ```java
         _client.notifyFailed(opportunity, UNSUPPORTED_OPERATION);
         ```

<!--<a id="example_463B718749504A978F0B887786844C39"></a>-->

Detta exempel på anpassad annonslösare löser ett problem och ger en enkel annons:

```java
public class CustomContentResolver extends ContentResolver { 
    protected void doConfigure(MediaPlayerItem item){} 
 
    protected boolean doCanResolve(Opportunity opportunity) {  
        return true;  
    } 
 
    protected void doResolve(Opportunity opportunity) { 
        _client.process(createAdBreakPlacementsFor(opportunity.getPlacement())); 
        _client.notifyCompleted(opportunity); 
    } 
 
    private List<TimelineOperation> createAdBreakPlacementsFor(Placement placementInformation) { 
        List<Ad> ads = new ArrayList<Ad>(); 
        AdAsset adAsset = new AdAsset("101", 15000, new MediaResource( 
          "https: . . ..m3u8", MediaResource.Type.HLS, null), null, null); 
 
        Ad ad = Ad.linearFromAsset("101", adAsset, null, null, false); 
        ads.add(ad); 
        AdBreak adBreak = new AdBreak(ads, null, AdInsertionType.CLIENT_INSERTED); 
 
        List<TimelineOperation> result = new ArrayList<TimelineOperation>(); 
 
        result.add(new AdBreakPlacement(placementInformation, adBreak)); 
        return result; 
    } 
 
    protected void doCleanup() {} 
} 
```

