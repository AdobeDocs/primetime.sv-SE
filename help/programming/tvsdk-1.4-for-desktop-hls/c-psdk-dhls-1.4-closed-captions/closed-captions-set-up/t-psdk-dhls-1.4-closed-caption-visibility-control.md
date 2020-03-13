---
description: Du kan styra synligheten för undertexter. När synligheten är aktiverad visas det markerade spåret. Om du ändrar vilket spår som är aktuellt ändras inte synlighetsinställningen.
seo-description: Du kan styra synligheten för undertexter. När synligheten är aktiverad visas det markerade spåret. Om du ändrar vilket spår som är aktuellt ändras inte synlighetsinställningen.
seo-title: Kontrollera synlighet för undertexter
title: Kontrollera synlighet för undertexter
uuid: 360d1158-67d9-40d9-b4b6-8ef46f9d73c0
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Kontrollera synlighet för undertexter{#control-closed-caption-visibility}

Du kan styra synligheten för undertexter. När synligheten är aktiverad visas det markerade spåret. Om du ändrar vilket spår som är aktuellt ändras inte synlighetsinställningen.

>[!TIP]
>
>Om undertextad text visas när spelaren går över till sökningsläget visas inte texten längre när sökningen har slutförts. Efter några sekunder visar i stället TVSDK nästa textning i videon efter den avslutande sökpositionen.

>[!NOTE]
>
>Synlighetsvärdena för undertexter definieras i `ClosedCaptionsVisibility`. >
>
```>
>public static const HIDDEN:String = hidden; 
>public static const VISIBLE:String = visible;
>```>



1. Vänta tills `MediaPlayer` statusen FÖRBEREDD är minst (se [Vänta på ett giltigt tillstånd](../../t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-state-prepared-wait-for.md)).
1. Om du vill hämta den aktuella synlighetsinställningen för undertexter använder du get-metoden i `MediaPlayer`, som returnerar ett synlighetsvärde.

   ```
   public function get ccVisibility():String
   ```

1. Om du vill ändra synligheten för undertexter använder du metoden set och skickar ett synlighetsvärde från `ClosedCaptionsVisibility`.

   Exempel:

   ```
   public function set ccVisibility(value:String):void
   ```

1. Definiera en nedrullningsbar lista.

   ```
   <s:DropDownList id="ccTracksList" width="85" 
                   dataProvider="{_ccTracks}" 
                   change="onCCTrackChange(event)" 
                   prompt="CC"/>
   ```

1. Definiera en bindningsbar array med textningsspår.

   ```
   [Bindable] private var _ccTracks:ArrayCollection =  
     new ArrayCollection(); // active tracks 
   ```

1. Konfigurera avlyssnare.

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.CAPTIONS_UPDATED, onCaptionUpdated);
   ```

   Så här tar du bort avlyssnarna från din destruktionskod:

   ```
   player.removeEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.removeEventListener(MediaPlayerItemEvent.CAPTIONS_UPDATED, onCaptionUpdated);
   ```

1. Skapa och uppdatera listan när en användare gör ett val i listan.

   ```
   private function onCCTrackChange(event:IndexChangeEvent):void { 
       var ccTrackIndex:int = event.newIndex; 
       var ccTracks:Vector.<ClosedCaptionsTrack> =  
         _player.currentItem.closedCaptionsTracks; 
       if (ccTrackIndex == 0) { 
           _player.ccVisibility = MediaPlayer.INVISIBLE; 
       } 
       else if (ccTrackIndex <= _ccTracks.length) { 
           var index:Number = findFromActiveIndex(ccTracks, ccTrackIndex - 1); 
           _player.currentItem.selectClosedCaptionsTrack(ccTracks[index]); 
           _player.ccVisibility = MediaPlayer.VISIBLE; 
       } 
   } 
   
   private function findFromActiveIndex(ccTracks:Vector.<ClosedCaptionsTrack>,  
     ccTrackIndex:int):Number { 
       var count:Number = 0; 
       for each (var ccTrack:ClosedCaptionsTrack in ccTracks) { 
           if (count < ccTrackIndex) 
               count = count + 1; 
           else 
               return count; 
       } 
       return -1; 
   } 
   
   private function onItemCreated(event:MediaPlayerItemEvent):void { 
       ... (you are likely to need more code here for other reasons) 
       updateCCTracks(_player.currentItem.closedCaptionsTracks); 
   } 
   
   private function onCaptionUpdated(event:MediaPlayerItemEvent):void { 
       ... (you are likely to need more code here for other reasons) 
       updateCCTracks(_player.currentItem.closedCaptionsTracks,  
                     (_player.ccVisibility == MediaPlayer.VISIBLE) ?  
                      _player.currentItem.selectedClosedCaptionsTrack : null); 
   } 
   
   private function updateCCTracks(tracks:Vector.<ClosedCaptionsTrack>,  
     selectedTrack:ClosedCaptionsTrack = null):void { 
       _ccTracks.removeAll(); 
   
       _ccTracks.addItem( 
           { 
               "label": "CC off", 
               "data": "cc-off" 
           } 
       ); 
   
       var selectedIndex:int = 0; 
       for each (var ccTrack:ClosedCaptionsTrack in tracks) { 
           _ccTracks.addItem( 
               { 
                   "label": ccTrack.name, 
                   "data": ccTrack.name 
               } 
           ); 
           if (selectedTrack && ccTrack.name == selectedTrack.name && 
           ccTrack.language == selectedTrack.language && 
           ccTrack.serviceType == selectedTrack.serviceType) { 
               selectedIndex = _ccTracks.length - 1; 
           } 
       } 
   
       var hasCC:Boolean = _ccTracks.length > 0; 
       ccTracksList.enabled = hasCC; 
       ccTracksList.mouseEnabled = hasCC; 
       ccTracksList.selectedIndex = selectedIndex; 
   } 
   ```

