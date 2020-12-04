---
description: Som standard tvingar TVSDK en annonsbrytning att spelas upp när användaren söker över en annonsbrytning. Du kan anpassa beteendet för att hoppa över en annonsbrytning om tiden som gått från en tidigare avbruten brytning är inom ett visst antal minuter.
seo-description: Som standard tvingar TVSDK en annonsbrytning att spelas upp när användaren söker över en annonsbrytning. Du kan anpassa beteendet för att hoppa över en annonsbrytning om tiden som gått från en tidigare avbruten brytning är inom ett visst antal minuter.
seo-title: Hoppa över annonsbrytningar under en tidsperiod
title: Hoppa över annonsbrytningar under en tidsperiod
uuid: 1a18d5fd-c957-481b-83ae-2129590c1678
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Hoppa över annonsbrytningar under en tidsperiod{#skip-ad-breaks-for-a-period-of-time}

Som standard tvingar TVSDK en annonsbrytning att spelas upp när användaren söker över en annonsbrytning. Du kan anpassa beteendet för att hoppa över en annonsbrytning om tiden som gått från en tidigare avbruten brytning är inom ett visst antal minuter.

>[!IMPORTANT]
>
>När det finns en intern sökning att hoppa över en annons kan det finnas en liten paus i uppspelningen.

Följande exempel på en anpassad annonsprincipväljare hoppar över annonser inom de kommande fem minuterna (väggklocka) efter att en användare har tittat på en annonsbrytning.

1. Utöka standardväljaren för annonsprinciper om du vill åsidosätta standardbeteendet.

   ```
   /** 
    * Custom ad policy selector. 
    */ 
   public class CustomAdPolicySelector extends DefaultAdPolicySelector { 
   
       /** 
        * Default constructor. 
        * 
        * @param item Associated media player item. 
        */ 
       public function CustomAdPolicySelector(item:MediaPlayerItem) { 
           super(item); 
   
           item.player.addEventListener(AdBreakPlaybackEvent.AD_BREAK_COMPLETED,  
                                        onAdBreakCompleted); 
       } 
   
       override public function selectPolicyForAdBreak(adPolicyInfo:AdPolicyInfo):String { 
           if (shouldPlayAds()) { 
               return super.selectPolicyForAdBreak(adPolicyInfo); 
           } 
   
           return AdBreakPolicy.SKIP; 
       } 
   
       override public function selectAdBreaksToPlay(adPolicyInfo:AdPolicyInfo):Vector.<AdBreakTimelineItem> { 
           if (shouldPlayAds()) { 
               return super.selectAdBreaksToPlay(adPolicyInfo); 
           } 
   
           return new Vector.<AdBreakTimelineItem>(); 
       } 
   
       override public function selectPolicyForSeekIntoAd(adPolicyInfo:AdPolicyInfo):String { 
           if (shouldPlayAds()) { 
               return super.selectPolicyForSeekIntoAd(adPolicyInfo); 
           } 
   
           return AdPolicy.SKIP_TO_NEXT_AD_IN_AD_BREAK; 
       } 
   
       private function onAdBreakCompleted(event:AdBreakPlaybackEvent):void { 
           _lastAdBreakPlayedTime = new Date().valueOf(); 
       } 
   
       private function shouldPlayAds():Boolean { 
           var currentTime:Number = new Date().valueOf(); 
           return isNaN(_lastAdBreakPlayedTime) 
                   ||  (currentTime - _lastAdBreakPlayedTime > _minimumInterval); 
       } 
   
       private var _lastAdBreakPlayedTime:Number = NaN; 
       private var _minimumInterval:Number = 300000; // 5 minutes in milliseconds 
   }
   ```

1. Skapa en ny reklamfabrik som använder din anpassade väljare.

   ```
   public class CustomAdPolicyContentFactory extends DefaultContentFactory { 
   
       private var _adPolicySelector:CustomAdPolicySelector; 
   
       /** 
        * Default constructor. 
        */ 
       public function CustomAdPolicyContentFactory() { 
   
       } 
   
       /** 
       * @inheritDoc 
       */ 
       override protected function doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
       if (!_adPolicySelector) { 
           _adPolicySelector = new CustomAdPolicySelector(item); 
       } 
   
       return _adPolicySelector; 
       } 
   }
   ```

1. Registrera den nya annonseringsfabriksklassen som ska användas med MediaPlayer.

   ```
   var mediaResource:MediaResource =  
     MediaResource.createFromUrl("https://example.org/stream.m3u8", null); 
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     PSDKConfig.retrieveMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomAdPolicyContentFactory(); 
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

