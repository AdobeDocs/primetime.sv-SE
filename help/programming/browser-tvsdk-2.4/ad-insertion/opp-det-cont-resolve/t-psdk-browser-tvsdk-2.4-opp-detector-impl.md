---
description: Du kan implementera en egen generator för affärsmöjligheter genom att utöka gränssnittet för OpportunityGenerator.
seo-description: Du kan implementera en egen generator för affärsmöjligheter genom att utöka gränssnittet för OpportunityGenerator.
seo-title: Implementera en generator för anpassade affärsmöjligheter
title: Implementera en generator för anpassade affärsmöjligheter
uuid: b80da2da-32d5-41f7-86ca-936d6f25b015
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 4%

---


# Implementera en generator för anpassad affärsmöjlighet{#implement-a-custom-opportunity-generator}

Du kan implementera en egen generator för affärsmöjligheter genom att utöka gränssnittet för OpportunityGenerator.

1. Skapa den anpassade affärsmöjlighetsgeneratorn.

   Exempel:

   ```js
   /** 
   * Class implementing AdobePSDK.OpportunityGenerator interface 
   */ 
   CustomOpportunityGenerator = function () { 
   }; 
   
   CustomOpportunityGenerator.prototype = { 
       constructor: CustomOpportunityGenerator, 
       configureCallbackFunc: function (item, client, mode, playhead, playbackRange) {  
           // the playhead represents the initial playback position 
           // the playback range represents the initial playback range 
   
           // the item property indicates the current AdobePSDK.MediaPlayerItem associated with this generator 
           // the initial set of timed metadata can be obtain through the item property 
           var timedMetadatas = item.timedMetadata; 
       }, 
       updateCallbackFunc: function (playhead, playbackRange) { 
           // when an opportunity is created by this generator 
           // we need to notify the TVSDK through the client property 
           client.resolve (opportunity); 
       }, 
       … 
   }; 
   ```

1. Skapa den anpassade innehållsfabriken som använder den anpassade affärsmöjlighetsgeneratorn.

   Exempel:

   ```js
   /** 
     * Class implementing AdobePSDK.ContentFactory interface 
   */ 
   CustomContentFactory = function () { 
   }; 
   
   CustomContentFactory.prototype = { 
          constructor: CustomContentFactory, 
          retrieveOpportunityGeneratorsCallbackFunc: function (item) { 
               var result = []; 
               result.push (new CustomOpportunityGenerator()); 
               return result; 
       }, 
       … 
   }; 
   ```

1. Registrera den anpassade innehållsfabriken för den medieström som ska spelas upp.

   I UI Framework Player kan du ange anpassad innehållsfabrik enligt följande:

   ```js
   var advertisingFactory = new CustomContentFactory(); 
   var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
           mediaPlayerItemConfig: { 
                   advertisingFactory: advertisingFactory 
           }, 
               mediaResource: { 
                   resourceUrl:'Specify Resource Url' 
          } 
     } 
   }); 
   ```

