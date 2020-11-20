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


# Styra videovyns placering och storlek{#control-the-position-and-size-of-the-video-view}

Du kan styra videovyns position och storlek med MediaPlayerView-objektet.

TVSDK försöker som standard att behålla videovyns proportioner när videons storlek eller position ändras (på grund av en ändring som gjorts av programmet, en profilväxel eller en innehållsväxel, osv.).

Du kan åsidosätta standardbeteendet för proportioner genom att ange en annan *skalpolicy*. Ange skalningsprincipen med hjälp av `MediaPlayerView` objektets `scalePolicy` egenskap. Standardskalningsprincipen `MediaPlayerView`anges med en instans av `MaintainAspectRatioScalePolicy` klassen. Om du vill återställa skalförändringsprincipen ersätter du standardinstansen av den `MaintainAspectRatioScalePolicy` med `MediaPlayerView.scalePolicy` din egen princip. (Du kan inte ange egenskapen till ett null-värde.) `scalePolicy`

1. Implementera `MediaPlayerViewScalePolicy` gränssnittet för att skapa en egen skalpolicy.

   Det `MediaPlayerViewScalePolicy` finns en metod:

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK använder ett `StageVideo` objekt för att visa videon, och eftersom `StageVideo` objekt inte finns med i visningslistan innehåller parametern `viewPort` de absoluta koordinaterna för videon.
   >
   >
   >Exempel:
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

1. Tilldela implementeringen till `MediaPlayerView` egenskapen.

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. Lägg till vyn i Media Players `view` egenskap.

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

