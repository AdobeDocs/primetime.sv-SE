---
description: Du kan implementera egna generatorer för affärsmöjligheter genom att implementera klassen OpportunityGenerator.
seo-description: Du kan implementera egna generatorer för affärsmöjligheter genom att implementera klassen OpportunityGenerator.
seo-title: Implementera en generator för anpassade affärsmöjligheter
title: Implementera en generator för anpassade affärsmöjligheter
uuid: 6a6a6aa4-51f8-4e3c-9255-d87b488b820d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Implementera en generator för anpassade affärsmöjligheter {#implement-a-custom-opportunity-generator}

Du kan implementera egna generatorer för affärsmöjligheter genom att implementera klassen OpportunityGenerator.

1. Implementera ditt eget gränssnitt `ContentFactory` genom att implementera `ContentFactory` gränssnittet och åsidosätta `retrieveGenerators`.

   Exempel:

   ```java
   class MyContentFactory extends ContentFactory { 
       @Override 
       public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
           List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
           generators.add(MyOpportunityGenerator(item)); 
           return generators; 
       } 
       ... 
   }
   ```

1. Registrera `ContentFactory` till `MediaPlayer`.

   Exempel:

   ```java
   // register the custom content factory with media player 
   MediaPlayerItemConfig config =  new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new MyContentFactory()); 
   
   // this config will should be later passed while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config); 
   
   // OR use MediaPlayerItemLoader to pre-load a resource 
   id = 23; 
   itemLoader.load(resource, id, config);
   ```

1. Skapa en anpassad klass för generering av affärsmöjlighet som implementerar `OpportunityGenerator` klassen.

   ```java
   public class CustomOpportunityGenerator implements OpportunityGenerator  
   {...}
   ```

   1. I den anpassade affärsmöjlighetsgeneratorn åsidosätter `doConfigure`och `doUpdate` `doCleanup`:

      ```java
      @Override 
       public void configure(MediaPlayerItem item, Context context,  
       OpportunityGeneratorClient client, AdSignalingMode mode, long playhead, TimeRange playbackRange) { 
      } 
      
      protected void update(long playhead, TimeRange playbackRange){ 
      } 
      
      protected void cleanup(){ 
      }
      ```

      Så här hämtar du tidsbestämda metadata:

      ```java
      List<TimedMetadata> tList = getItem().getTimedMetadata(); 
      ```

   1. Skapa en affärsmöjlighet med följande attribut för varje `TimedMetadata` eller grupp av `TimedMetadata`:

      ```java
      Opportunity( 
        String id,                      // Can be id from timedMetadata  
        Placement placementInformation, // Placement object containing Type, time, duration 
        Metadata metadataSettings,      // Ad metadata with targeting params sent to the ad provider 
        Metadata customParams           // Metadata for customizing resolving and/or tracking process. 
      ); 
      ```

   1. För varje affärsmöjlighet som skapas, ring `resolve` på `OpportunityGeneratorClient:getClient().resolve(opportunity);`.

<!--<a id="example_7A46377EBE79458E87423EB95D0568D4"></a>-->

Detta är ett exempel på identifierare av anpassade placeringsmöjligheter:

```java
public class MyOpportunityGenerator implements OpportunityGenerator {

     @Override 
      public void configure(MediaPlayerItem item, Context context,  
      OpportunityGeneratorClient client, AdSignalingMode mode, long playhead, TimeRange playbackRange) { 
      } 
 
        MediaPlayerItem item = getItem(); 
        MediaPlayerItemConfig itemConfig = item.getConfig(); 
 
        if (itemConfig == null || itemConfig.getAdvertisingMetadata() == null) { 
            // no ad metadata, no ads 
            return; 
        } 
 
        AdvertisingMetadata metadata = item.getConfig().getAdvertisingMetadata();

        AdSignalingMode mode = itemConfig.getAdSignalingMode(); 
 
        if (mode == AdSignalingMode.CUSTOM_RANGES) 
        { 
            // don't override custom ad ranges 
            return; 
        } 
 
        Placement.Type pType = (mode == AdSignalingMode.MANIFEST_CUES) ?  
                  Placement.Type.PRE_ROLL : Placement.Type.SERVER_MAP; 
        Placement.Mode pMode = Placement.Mode.DEFAULT; 
        Placement placement = new Placement(pType, playhead,  
                  Placement.UNKNOWN_DURATION, pMode); 
 
        Opportunity opportunity = new Opportunity("initialOpportunity", placement,  
                  metadata, null); 
 
        OpportunityGeneratorClient client = getClient(); 
        client.resolve(opportunity); 
    } 
 
    @Override 
    protected void update(long playhead, TimeRange playbackRange) { 
 
 ... 
 timedMetadataList = getItem().getTimedMetadata(); 
        for (TimedMetadata timedMetadata : timedMetadataList) { 
         if (isOpportunity(timedMetadata)) {   // check if given timedMetadata should  
                                               // be considered as an opportunity 
  // create a PlacementOpportunity object and add it to the opportunities list 
                Opportunity opportunity = new Opportunity("id", placement, metadata, null); 
                client.resolve(opportunity) 
          } 
        } 
    } 
 
    @Override 
    protected void cleanup() {} 
}
```
