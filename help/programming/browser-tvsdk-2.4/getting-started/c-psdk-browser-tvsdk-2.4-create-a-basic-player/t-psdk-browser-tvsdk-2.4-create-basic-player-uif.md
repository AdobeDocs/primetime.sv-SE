---
title: Skapa en grundläggande spelare med UI Framework
description: Skapa en grundläggande spelare med UI Framework
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 1%

---


# Skapa en grundläggande spelare med UI Framework{#create-a-basic-player-using-the-ui-framework}

Så här skapar du en grundläggande spelare med hjälp av UI-ramverket:

1. Skapa en `<div>` för spelarinstansen.

   Exempel:

   ```
   <div id="video1" > 
    </div>
   ```

1. Läs in spelaren.

   ```js
   <script> 
       (function(){ 
           var player = ptp.videoPlayer('#video1'); 
       })(); 
   </script>
   ```

   När spelaren skapas får det angivna `<div>`-elementet CSS-klassen `ptp-main-video-div-style`. Den resulterande DOM ser ut ungefär så här:

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. Lägg till en gränssnittskontroll.

   Lägg till exempel till ett kontrollfält som visas när muspekaren förs över spelaren:

   ```js
   <script> 
       (function(){ 
           function myControlBarBehavior(element, configuration, player) { 
               return ptp.controlBarBehavior(element, configuration, player); 
           } 
           var player = ptp.videoPlayer('#video1', { 
               controlBar: { 
                   behavior: myControlBarBehavior, 
                   classNames: 'ptp-control-bar my_control_bar' 
               } 
           }); 
       })(); 
   </script>
   ```

   Den resulterande DOM-filen visas enligt följande:

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <div class="ptp-control-bar my_control_bar"></div> 
       <video class="vp-video-element"></video> 
   </div>
   ```

Objektet som returneras från anrop av `ptp.videoPlayer()` ger ett beteende som omsluter TVSDK-mediespelarens API och möjliggör programmatisk styrning av uppspelningen. När du anropar mediespelarinstansen uppdateras användargränssnittet automatiskt baserat på händelser som utlöses av mediespelaren:

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
