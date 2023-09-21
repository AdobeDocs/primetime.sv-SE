---
description: Du kan styra videovyns position och storlek med MediaPlayerView-objektet.
title: Styra videovyns placering och storlek
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Styra videovyns placering och storlek{#control-the-position-and-size-of-the-video-view}

Du kan styra videovyns position och storlek med MediaPlayerView-objektet.

TVSDK försöker som standard att behålla videovyns proportioner när videons storlek eller position ändras (på grund av en ändring som gjorts av programmet, en profilväxel eller en innehållsväxel etc.).

Du kan åsidosätta standardbeteendet för proportioner genom att ange ett annat *skalningsprofil*. Ange skalningsprincipen med `MediaPlayerView` objektets `scalePolicy` -egenskap. The `MediaPlayerView`Standardskalningsprincipen anges med en instans av `MaintainAspectRatioScalePolicy` klassen. Om du vill återställa skalprincipen ersätter du standardinstansen av `MaintainAspectRatioScalePolicy` på `MediaPlayerView.scalePolicy` med er egen policy. (Du kan inte ange `scalePolicy` till ett null-värde.)

1. Implementera `MediaPlayerViewScalePolicy` för att skapa en egen skalpolicy.

   The `MediaPlayerViewScalePolicy` har en metod:

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK använder en `StageVideo` -objekt för att visa videon, och därför `StageVideo` objekten inte finns med i visningslistan, `viewPort` -parametern innehåller videons absoluta koordinater.
   >
   >
   >Till exempel:
   >
   >```
   >public class CustomScalePolicy implements MediaPlayerViewScalePolicy { 
   >       /** 
   >         * Default constructor. 
   >         */ 
   >       public function CustomScalePolicy() { 
   >       } 
   > 
   >    
      public function adjust(viewPort:Rectangle,  
   >                                                     videoWidth:Number,  
   >                                                     videoHeight:Number):Rectangle { 
   >               return customAdjustment(); 
   >       } 
   > 
   >    
      public function customAdjustment():Rectangle { 
   >               /* Your custom adjustment here */ 
   >               [...] 
   >       } 
   >}
   >```
   >

1. Tilldela implementeringen till `MediaPlayerView` -egenskap.

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. Lägg till din vy i Mediespelarens `view` -egenskap.

   ```
   addChild(view); 
   
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**Exempel: Skala videon så att den fyller hela videovyn utan att behålla proportionerna:**

```
package com.adobe.mediacore.samples.utils { 
    import com.adobe.mediacore.view.MediaPlayerViewScalePolicy; 
    import flash.geom.Rectangle; 
 
    /** 
    * A very simple custom scale policy - the video will fill the entire 
    * allocated space. The aspect ratio will not be kept. 
    */ 
    public class CustomScalePolicy implements MediaPlayerViewScalePolicy { 
 
        /** 
        * Default constructor. 
        */ 
        public function CustomScalePolicy() { 
        } 
 
        public function adjust(viewPort:Rectangle, 
                               videoWidth:Number,  
                               videoHeight:Number):Rectangle { 
            return viewPort; 
        } 
    } 
} 
 
var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
view.scalePolicy = new CustomScalePolicy(); 
addChild(view); 
mediaPlayer.view = view;
```
