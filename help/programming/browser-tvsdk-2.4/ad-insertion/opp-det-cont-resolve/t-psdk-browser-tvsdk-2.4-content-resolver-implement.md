---
description: Du kan implementera egna innehållslösningar baserat på standardlösare.
seo-description: Du kan implementera egna innehållslösningar baserat på standardlösare.
seo-title: Implementera en anpassad innehållshanterare
title: Implementera en anpassad innehållshanterare
uuid: cf85dd90-242e-4f9e-9785-158ca0fc9465
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Implementera en anpassad innehållshanterare{#implement-a-custom-content-resolver}

Du kan implementera egna innehållslösningar baserat på standardlösare.

När Browser TVSDK identifierar en ny affärsmöjlighet itereras den igenom det registrerade innehållet för att hitta en som kan lösa den affärsmöjligheten med hjälp av `canResolve` metoden. Den första som returnerar true väljs för att matcha affärsmöjligheten. Om ingen innehållslösare kan användas hoppas den möjligheten över. Eftersom innehållsmatchningsprocessen vanligtvis är asynkron ansvarar innehållslösaren för att meddela webbläsarens TVSDK när processen har slutförts.

Kom ihåg följande information:

* Innehållslösaren anropar `client.process` för att ange vilken tidslinjeåtgärd som TVSDK måste utföra.

   Åtgärden är vanligtvis en annonsbrytningsplacering.

* Innehållslösaren anropar `client.notifyCompleted` om lösningsprocessen lyckas eller `client.notifyFailed` om processen misslyckas.

1. Skapa en anpassad lösare för affärsmöjligheter.

   ```js
   /** 
     * Class implementing AdobePSDK.ContentResolver interface  
   */ 
   CustomResolver = function () { 
   }; 
   
   CustomResolver.prototype = { 
       constructor: CustomResolver, 
       configureCallbackFunc: function (item, client) { 
       // here you can read any media stream characteristics which 
       // might help configure your content resolver like 
       // - the media player item configuration through the item.config 
       // - the media resource metadata through item.resource.metadata 
      }, 
   
       canResolveCallbackFunc: function (opportunity) { 
       // check if the opportunity can be resolved by this resolver 
       // if yes return true, otherwise return false 
       return true; 
      }, 
   
       resolveCallbackFunc: function (opportunity) {         
       // start the resolving process 
       // communicate with your custom ad server 
   
       // in this example we assume that: 
       // - if successful, onResolveCompleted method will be invoked 
       // - if failed, onResolveFailed method will be invoked 
      }, 
   
       onResolveCompleted: function (response) { 
        try { 
           var proposals = []; 
           // extract the timeline ad placement from the response 
           // and add them to the proposal vector 
           // - extract the ad break 
           // - calculate the placement (can reuse the _opportunity.placement) 
           // var timelineOperation = new AdobePSDK.AdBreakPlacement (adBreak, placement); 
           // proposals.push (timelineOperation); 
   
           client.process (proposals); 
           client.notifyCompleted (_opportunity); 
       } catch (error) { 
           onResolveFailed (error); 
       } 
   }, 
   
       onResolveFailed: function (error) { 
         client.notifyFailed (_opportunity); 
       } 
   
   }; 
   ```

1. Skapa den anpassade innehållsfabriken som använder den anpassade innehållslösaren.

   Exempel:

   ```js
   /** 
     * Class implementing AdobePSDK.ContentFactory interface 
   */ 
   CustomContentFactory = function () { 
   }; 
   
   CustomContentFactory.prototype = { 
       constructor: CustomContentFactory, 
       retrieveResolversCallbackFunc: function (item) { 
           var result = []; 
           var resource = item.resource; 
           if (resource.metadata.containsKey("custom-opportunity-detector")) { 
               result.push (new CustomResolver()); 
           } 
           return result; 
       }, 
       … 
   }; 
   ```

1. Registrera den anpassade innehållsfabriken för den medieström som ska spelas upp.

   I UI Framework Player kan du ange anpassad innehållsfabrik enligt följande:

   ```js
   var advertisingFactory = new CustomContentFactory(); 
   var advertisingMetadata = new AdobePSDK.AdvertisingMetadata(); 
   // set any parameter you need for custom ad resolver 
   // advertisingMetadata.setValue ("customparam", "customvalue"); 
   
   var metadata = new AdobePSDK.Metadata(); 
   metadata.setMetadata ("custom-opportunity-detector", advertisingMetadata); 
   
   var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
       mediaPlayerItemConfig: { 
              advertisingFactory: advertisingFactory 
       }, 
          mediaResource: { 
                  resourceUrl:'Specify Resource Url', 
                  metadata: metadata 
          } 
   } 
   
   }); 
   ```

