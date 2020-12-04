---
description: Du kan styra videovyns position och storlek med MediaPlayerView-objektet.
seo-description: Du kan styra videovyns position och storlek med MediaPlayerView-objektet.
seo-title: Styra videovyns placering och storlek
title: Styra videovyns placering och storlek
uuid: 2231c574-03cd-45a8-ab00-4a42f8e044f0
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Styra position och storlek för videovyn{#control-the-position-and-size-of-the-video-view}

Du kan styra videovyns position och storlek med MediaPlayerView-objektet.

TVSDK försöker som standard att behålla videovyns proportioner när videons storlek eller position ändras (på grund av en ändring som gjorts av programmet, en profilväxel eller en innehållsväxel, osv.).

Du kan åsidosätta standardbeteendet för proportioner genom att ange en annan *skalprincip*. Ange skalningsprincipen med `MediaPlayerView`-objektets `scalePolicy`-egenskap. Standardskalningsprincipen för `MediaPlayerView` anges med en instans av klassen `MaintainAspectRatioScalePolicy`. Om du vill återställa skalprincipen ersätter du standardinstansen av `MaintainAspectRatioScalePolicy` på `MediaPlayerView.scalePolicy` med din egen princip. (Du kan inte ange egenskapen `scalePolicy` till ett null-värde.)

1. Implementera gränssnittet `MediaPlayerViewScalePolicy` för att skapa en egen skalpolicy.

   `MediaPlayerViewScalePolicy` har en metod:

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK använder ett `StageVideo`-objekt för att visa videon, och eftersom `StageVideo`-objekt inte finns med i visningslistan innehåller parametern `viewPort` videons absoluta koordinater.
   >
   >
   >Exempel:
   >
   >
   ```
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

1. Tilldela din implementering till egenskapen `MediaPlayerView`.

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. Lägg till vyn i mediespelarens `view`-egenskap.

   ```
   addChild(view); 
   
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**Till exempel: Skala videon så att den fyller hela videovyn utan att behålla proportionerna:**

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

