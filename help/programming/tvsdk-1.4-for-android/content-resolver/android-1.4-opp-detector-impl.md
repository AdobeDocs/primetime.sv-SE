---
description: Du kan implementera egna affärsmöjlighetsdetektorer genom att implementera gränssnittet PlacementOpportunityDetector.
title: Implementera en anpassad affärsmöjlighetsdetektor
exl-id: d78949a0-2c76-4976-9358-05f3db86781e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Implementera en anpassad affärsmöjlighetsdetektor {#implement-a-custom-opportunity-detector}

Du kan implementera egna affärsmöjlighetsdetektorer genom att implementera gränssnittet PlacementOpportunityDetector.

1. Skapa en egen `AdvertisingFactory` instans och åsidosättning `createOpportunityDetector`. Till exempel:

   ```java
   new AdvertisingFactory() { 
       ... 
       @Override 
       public PlacementOpportunityDetector createOpportunityDetector(MediaPlayerItem item) { 
           return new CustomPlacementOpportunityDetector(); 
       } 
       ... 
   }
   ```

1. Registrera annonsklientfabriken på `MediaPlayer`. Till exempel:

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. Skapa en anpassad klass för affärsmöjlighetsdetektor som utökar `PlacementOpportunityDetector` klassen.
   1. Åsidosätt den här funktionen i den anpassade affärsmöjlighetsidentifieraren:

      ```java
      public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata)
      ```

      The `timedMetadataList` innehåller listan med tillgängliga `TimedMetadata`, som sorteras. Metadata innehåller målparametrar och anpassade parametrar som ska skickas till annonsleverantören.

   1. För varje `TimedMetadata`, skapa `List<PlacementOpportunity>`. Listan kan vara tom, men inte null. `PlacementOpportunity` ska ha följande attribut:

      ```java
      PlacementOpportunity( 
          String id,                                      // can be id from timedMetadata 
          PlacementInformation placementInformation   // PlacementInformation object containing Type, time, duration 
          Metadata metadata                           // ad metadata containing targeting params sent to the ad provider 
      )
      ```

   1. När placeringsmöjligheter har skapats för alla identifierade tidsbestämda metadataobjekt returnerar du bara `PlacementOpportunity` lista.

Detta är ett exempel på identifierare av anpassade placeringsmöjligheter:

```java
public class CustomPlacementOpportunityDetector implements PlacementOpportunityDetector { 
    ... 
    @Override 
    public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata) { 
        ... 
        List<PlacementOpportunity> opportunities = new ArrayList<PlacementOpportunity>(); 
 
        for (TimedMetadata timedMetadata : timedMetadataList) { 
 
            if (isOpportunity(timedMetadata)) {        // check if given timedMetadata should be  
                                                       // considered as an opportunity 
 
                // create an object of PlacementOpportunity and add it to the opportunities list 
                PlacementOpportunity opportunity =  
                  createPlacementOpportunity(timedMetadata, airingId, metadata); 
                Opportunities.add(opportunity); 
            } 
        } 
        return opportunities; 
    }    
    ... 
} 
```
