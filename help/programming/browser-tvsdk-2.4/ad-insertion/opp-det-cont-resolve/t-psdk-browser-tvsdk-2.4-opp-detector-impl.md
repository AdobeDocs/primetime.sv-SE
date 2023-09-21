---
description: Du kan implementera en egen generator för affärsmöjligheter genom att utöka gränssnittet för OpportunityGenerator.
title: Implementera en generator för anpassade affärsmöjligheter
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Implementera en generator för anpassade affärsmöjligheter{#implement-a-custom-opportunity-generator}

Du kan implementera en egen generator för affärsmöjligheter genom att utöka gränssnittet för OpportunityGenerator.

1. Skapa den anpassade affärsmöjlighetsgeneratorn.

   Till exempel:

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

   Till exempel:

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
