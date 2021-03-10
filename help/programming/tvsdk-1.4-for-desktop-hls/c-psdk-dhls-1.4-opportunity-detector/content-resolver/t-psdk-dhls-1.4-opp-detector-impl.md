---
description: Ni kan implementera egna affärsmöjlighetsdetektorer.
title: Implementera en anpassad affärsmöjlighetsdetektor
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Implementera en anpassad affärsmöjlighetsdetektor{#implement-a-custom-opportunity-detector}

Ni kan implementera egna affärsmöjlighetsdetektorer.

* Om din affärsmöjlighetsgenerator baseras på `TimedMetadata`-objekt som är associerade med den aktuella medieströmmen bör den utöka `SpliceOutOpportunityGenerator` eller `TimedMetadataOpportunityGenerator`.

* Om affärsmöjlighetsgeneratorn är baserad på out-of-band-data som tillhandahålls av en extern tjänst (till exempel en CIS), bör den utöka `OpportunityGenerator`.

1. Skapa den anpassade affärsmöjlighetsgeneratorn.

       Om den anpassade generatorn för affärsmöjlighet är baserad på TimedMetadata-objekt, utökar du TimedMetadataOpportunityGenerator och åsidosätter dessa metoder:
   
   * `doConfigure` - Den här metoden anropas efter att mediespelarobjektet har skapats och ger möjlighet att skapa en första uppsättning möjligheter vid behov
   * `doProcess` - Den här metoden anropas varje gång nya  `TimedMetadata` upptäcks (t.ex. för live/linear-strömmar varje gång spellistan/manifestet uppdateras)

   ```
   public class CustomOpportunityGenerator extends TimedMetadataOpportunityGenerator { 
       override protected function doConfigure(playhead:Number, playbackRange:TimeRange):void { 
           // the playhead represents the initial playback position 
           // the playback range represents the initial playback range 
   
           // the item property indicates the current MediaPlayerItem associated with this generator 
           // the initial set of timed metadata can be obtain through the item property 
           var timedMetadataCollection:Vector.<TimedMetadata> = item.timedMetadata; 
       } 
   
       override protected function doProcess(timedMetadata:TimedMetadata):void { 
           ... 
   
           // when an opportunity is created by this generator 
           // we need to notify the TVSDK through the client property 
           client.resolve(opportunity); 
       }  
       ... 
   }
   ```

1. Skapa den anpassade innehållsfabriken som använder den anpassade affärsmöjlighetsgeneratorn.

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
       ... 
   
       /** 
       * @inheritDoc 
       */ 
       override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
           var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
           result.push(new CustomOpportunityGenerator()); 
   
           return result; 
       } 
   }
   ```

1. Registrera den anpassade innehållsfabriken för den medieström som ska spelas upp.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

