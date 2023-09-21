---
description: Du kan styra videovyns position och storlek med MediaPlayerView-objektet.
title: Styra videovyns placering och storlek
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Styra videovyns placering och storlek{#control-the-position-and-size-of-the-video-view}

Du kan styra videovyns position och storlek med MediaPlayerView-objektet.

Webbläsaren TVSDK försöker som standard att behålla videovyns proportioner när storleken eller positionen för videon ändras på grund av en ändring som gjorts av programmet, en profilväxling, en innehållsväxling osv.

Du kan åsidosätta standardbeteendet för proportioner genom att ange ett annat *skalningsprofil*. Ange skalningsprincipen med `MediaPlayerView` objektets `scalePolicy` -egenskap. Standardskalningsprincipen för `MediaPlayerView` anges med en instans av `MaintainAspectRatioScalePolicy` klassen. Om du vill återställa skalprincipen ersätter du standardinstansen av `MaintainAspectRatioScalePolicy` på `MediaPlayerView.scalePolicy` med er egen policy.

>[!IMPORTANT]
>
>Du kan inte ange `scalePolicy` till ett null-värde.

## Fallscenarier som inte är Flashar {#non-flash-fallback-scenarios}

För att skalningsprincipen ska fungera korrekt i andra scenarier än Flashar anges video-div-elementet i `View` konstruktorn ska returnera värden som inte är noll för `offsetWidth` och `offsetHeight`. Om du vill ge ett exempel på en felaktig funktion, ibland när bredden och höjden på video-div-elementen inte anges explicit i css, kommer `View` konstruktorn returnerar noll för `offsetWidth` eller `offsetHeight`.

>[!NOTE]
>
>CustomScalePolicy har begränsat stöd för några webbläsare, bland annat IE, Edge och Safari 9. För dessa webbläsare går det inte att ändra videofilens ursprungliga proportioner. Videons position och dimensioner används dock enligt skalningsprincipen.

1. Implementera `MediaPlayerViewScalePolicy` för att skapa en egen skalpolicy.

   The `MediaPlayerViewScalePolicy` har en metod:

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

   Till exempel:

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

1. Tilldela implementeringen till `MediaPlayerView` -egenskap.

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. Lägg till din vy i Mediespelarens `view` -egenskap.

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**Exempel: Skala videon så att den fyller hela videovyn utan att behålla proportionerna:**

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
