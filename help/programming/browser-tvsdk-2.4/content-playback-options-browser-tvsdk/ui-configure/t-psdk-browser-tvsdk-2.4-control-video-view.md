---
description: Du kan styra videovyns position och storlek med MediaPlayerView-objektet.
seo-description: Du kan styra videovyns position och storlek med MediaPlayerView-objektet.
seo-title: Styra videovyns placering och storlek
title: Styra videovyns placering och storlek
uuid: d09dbc18-1ec0-4336-bf3f-7ff6c265c443
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Styra videovyns placering och storlek{#control-the-position-and-size-of-the-video-view}

Du kan styra videovyns position och storlek med MediaPlayerView-objektet.

Webbläsaren TVSDK försöker som standard att behålla videovyns proportioner när storleken eller positionen för videon ändras på grund av en ändring som gjorts av programmet, en profilväxling, en innehållsväxling osv.

Du kan åsidosätta standardbeteendet för proportioner genom att ange en annan *skalpolicy*. Ange skalningsprincipen med hjälp av `MediaPlayerView` objektets `scalePolicy` egenskap. Standardskalningsprincipen för `MediaPlayerView` anges med en instans av `MaintainAspectRatioScalePolicy` klassen. Om du vill återställa skalförändringsprincipen ersätter du standardinstansen av den `MaintainAspectRatioScalePolicy` med `MediaPlayerView.scalePolicy` din egen princip.

>[!IMPORTANT]
>
>Du kan inte ställa in egenskapen på ett null-värde. `scalePolicy`

## Utfallsscenarier som inte är Flash {#non-flash-fallback-scenarios}

För att skalningsprincipen ska fungera korrekt i andra scenarier än Flash-reservscenarier bör video-div-elementet som anges i konstruktorn returnera värden som inte är noll för `View` och `offsetWidth` `offsetHeight`. Om du vill ge ett exempel på en felaktig funktion, ibland när bredden och höjden på video-div-elementen inte anges explicit i css, returnerar konstruktorn `View` noll för `offsetWidth` eller `offsetHeight`.

>[!NOTE]
>
>CustomScalePolicy har begränsat stöd för ett fåtal webbläsare, bland annat IE, Edge och Safari 9. För dessa webbläsare går det inte att ändra videofilens ursprungliga proportioner. Videons position och dimensioner används dock enligt skalningsprincipen.

1. Implementera `MediaPlayerViewScalePolicy` gränssnittet för att skapa en egen skalpolicy.

   Det `MediaPlayerViewScalePolicy` finns en metod:

   ```js
   /** 
   * Adjust the specified rectangle to match the new video dimensions. 
   * @param viewPort {AdobePSDK.Rectangle}The video rectangle as absolute position. 
   * @param videoWidth {Number}The video width. 
   * @param videoHeight {Number} The video height. 
   * @return {AdobePSDK.Rectangle} an adjusted rectangle. 
   */ 
   function adjustCallbackFunc(viewPort, videoWidth, videoHeight);
   ```

   Exempel:

   ```js
   /** 
   Default Constructor 
   */ 
   MediaPlayerViewCustomScalePolicy = function() { 
       return this; 
   }; 
   MediaPlayerViewCustomScalePolicy.prototype = { 
       constructor: MediaPlayerViewScalePolicy, 
       adjustCallbackFunc: function(viewPort, videoWidth, videoHeight) { 
           /* Your Custom Adjustment here. */ 
           [...] 
           return adjustedRectangle; 
       } 
   };
   ```

1. Tilldela implementeringen till `MediaPlayerView` egenskapen.

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. Lägg till vyn i Media Players `view` egenskap.

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**Till exempel: Skala videon så att den fyller hela videovyn utan att behålla proportionerna:**

```
/** 
 * Default constructor. 
 */ 
MediaPlayerViewCustomScalePolicy = function() { 
    return this; 
}; 
MediaPlayerViewCustomScalePolicy.prototype = { 
    constructor: MediaPlayerViewScalePolicy, 
    /** 
    * A very simple custom scale policy - the video will fill the entire 
    * allocated space. The aspect ratio will not be kept. 
    */ 
    adjustCallbackFunc: function(viewPort, videoWidth, videoHeight) { 
        return viewPort; 
    } 
}; 
var view = new AdobePSDK.MediaPlayerView(videoDiv); 
view.scalePolicy = new MediaPlayerViewCustomScalePolicy (); 
mediaPlayer.view = view;
```

