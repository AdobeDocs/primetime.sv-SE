---
description: Du kan använda Browser TVSDK för att hämta information om media som du kan visa i sökfältet.
title: Visa videons varaktighet, aktuella tid och återstående tid
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# Visa videons varaktighet, aktuella tid och återstående tid{#display-the-duration-current-time-and-remaining-time-of-the-video}

Du kan använda Browser TVSDK för att hämta information om media som du kan visa i sökfältet.

1. Vänta tills spelaren är i åtminstone tillståndet PREPARED.
1. Hämta den aktuella spelhuvudstiden med `MediaPlayer.currentTime` -attribut.

   Det här attributet returnerar spelhuvudets aktuella position på den virtuella tidslinjen i millisekunder. Tiden beräknas i förhållande till den matchade strömmen som kan innehålla flera instanser av alternativt innehåll, till exempel flera annonser eller annonsbrytningar som delas upp i huvudströmmen. För live-/linjära strömmar är den returnerade tiden alltid i uppspelningsfönsterintervallet.

   ```js
   MediaPlayer.currentTime
   ```

1. Hämta uppspelningsintervallet för strömmen och fastställ varaktigheten.
   1. Använd  `mediaPlayer.playbackRange` för att hämta tidsintervallet för den virtuella tidslinjen.

   1. Ta bort början från intervallets slut om du vill bestämma varaktigheten.

      Detta omfattar längden på ytterligare innehåll som infogas i strömmen (annonser).

      För VOD börjar intervallet alltid med noll och slutvärdet är lika med summan av innehållets längd och varaktigheten för ytterligare innehåll som infogas i flödet (annonser).

      För en linjär/liveresurs representerar intervallet uppspelningsfönstret och det här intervallet ändras under uppspelningen.

1. Använd de metoder som är tillgängliga i MediaPlayer- och Browser TVSDK-elementen för att ställa in sökfältsparametrarna.

   Här är t.ex. en möjlig layout för att visa sökfältet i HTML.

   ```
   <div class="seekbar" id="seekbar"> 
        <div> 
           <span class="backer" id="backer"></span> 
           <span class="buffer" id="buffer" ></span> 
           <div class="playhead" id="playhead"></div> 
                     <span class="progress" id="progress" ></span> 
           </div> 
         </div> 
     </div> 
   ```

   Här är motsvarande css:

   ```
   #seekbar { 
         position: relative; 
         width: 100%; 
         height: 16px; 
         cursor: pointer; 
         background: transparent; 
   } 
   
   #seekbar div { 
         position: relative; 
         height: 100%; 
         margin-left: 8px; 
         margin-right: 8px; 
   } 
   
   #seekbar span { 
         position: absolute; 
         height: 60%; 
         top: 20%; 
   
         display: block; 
   
         -webkit-border-radius: 16px; 
         -moz-border-radius: 16px; 
         border-radius: 16px; 
   } 
   
   #seekbar.playhead { 
        z-index: 1011; 
        height: 14px; 
        width: 14px; 
        border: 1px outset #c9cbce; 
        position: absolute; 
        left: -8px; /* adjust center of playhead over start of range */ 
        display: block; 
        padding: 0; 
        margin: 0; 
   
        background: #c9cbce; /* Old browsers */ 
        background: -moz-radial-gradient(circle, #4591ce 0%, #3080c2 40%, #c9cbce 45%, #dedee1 100%); /* FF3.6+ */ 
        background: -webkit-radial-gradient(circle, #4591ce 0%, #3080c2 40%, #c9cbce 45%, #dedee1 100%); /* Chrome10+,Safari5.1+ */ 
        background: -o-radial-gradient(circle, #4591ce 0%, #3080c2 40%, #c9cbce 45%, #dedee1 100%); /* Opera 11.10+ */ 
        background: -ms-radial-gradient(circle, #4591ce 0%, #3080c2 40%, #c9cbce 45%, #dedee1 100%); /* IE10+ */ 
        background: radial-gradient(circle, #4591ce 0%, #3080c2 40%, #c9cbce 45%, #dedee1 100%); /* W3C */ 
        filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#c9cbce', endColorstr='#dedee1',GradientType=0 ); /* IE6-9 */ 
   
        -webkit-border-radius: 16px; 
        -moz-border-radius: 16px; 
        border-radius: 16px; 
   } 
   
   #seekbar.backer { 
           z-index: 1004; 
           width: 100%; 
   
           background: #414142; /* Old browsers */ 
           background: -moz-linear-gradient(top,  #414142 0%, #343232 100%); /* FF3.6+ */ 
           background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#414142), color-stop(100%,#343232)); /* Chrome,Safari4+ */ 
           background: -webkit-linear-gradient(top,  #414142 0%,#343232 100%); /* Chrome10+,Safari5.1+ */ 
           background: -o-linear-gradient(top,  #414142 0%,#343232 100%); /* Opera 11.10+ */ 
           background: -ms-linear-gradient(top,  #414142 0%,#343232 100%); /* IE10+ */ 
           background: linear-gradient(to bottom,  #414142 0%,#343232 100%); /* W3C */ 
           filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#414142', endColorstr='#343232',GradientType=0 ); /* IE6-9 */ 
   
   } 
   
   #seekbar .buffer { 
          z-index: 1005; 
          position: absolute; 
   
          background: #4b4b4c; /* Old browsers */ 
          background: -moz-linear-gradient(top,  #4b4b4c 0%, #818184 100%); /* FF3.6+ */ 
          background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#4b4b4c), color-stop(100%,#818184)); /* Chrome,Safari4+ */ 
          background: -webkit-linear-gradient(top,  #4b4b4c 0%,#818184 100%); /* Chrome10+,Safari5.1+ */ 
          background: -o-linear-gradient(top,  #4b4b4c 0%,#818184 100%); /* Opera 11.10+ */ 
          background: -ms-linear-gradient(top,  #4b4b4c 0%,#818184 100%); /* IE10+ */ 
          background: linear-gradient(to bottom,  #4b4b4c 0%,#818184 100%); /* W3C */ 
          filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#4b4b4c', endColorstr='#818184',GradientType=0 ); /* IE6-9 */ 
   } 
   
   #seekbar .progress { 
           z-index: 1010; 
           position: absolute; 
   
           background: #4591ce; /* Old browsers */ 
           background: -moz-linear-gradient(top,  #4591ce 0%, #3080c2 100%); /* FF3.6+ */ 
           background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#4591ce), color-stop(100%,#3080c2)); /* Chrome,Safari4+ */ 
           background: -webkit-linear-gradient(top,  #4591ce 0%,#3080c2 100%); /* Chrome10+,Safari5.1+ */ 
           background: -o-linear-gradient(top,  #4591ce 0%,#3080c2 100%); /* Opera 11.10+ */ 
           background: -ms-linear-gradient(top,  #4591ce 0%,#3080c2 100%); /* IE10+ */ 
           background: linear-gradient(to bottom,  #4591ce 0%,#3080c2 100%); /* W3C */ 
           filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#4591ce', endColorstr='#3080c2',GradientType=0 ); /* IE6-9 */ 
   } 
   ```

1. Lyssna efter `AdobePSDK.TimeChangeEvent` och uppdatera sökfältet därefter.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIME_CHANGED, onTimeChange); 
   
   /** 
        * Called when the player's time changes. 
        * Update UI to show current time, seekbar playhead position and buffer level. 
        */ 
        function onTimeChange(event) 
        { 
          if (!seekBar.isSeeking) { 
          var time = event.time; 
          var range = player.playbackRange; 
          seekBar.updatePlayhead(time, range); 
          updateDisplayTime(time, range); 
   
           var bufferedRange = player.bufferedRange; 
           seekBar.updateBufferLevel(bufferedRange.end, range); 
         } 
   
       } 
   ```

   I det här exemplet skapas ett sökfältsobjekt för att uppdatera sökfältet:

   ```js
   /** 
       * Seekbar object which handles the display of the player progress,  
       * playhead, and buffer level. 
       */ 
       seekBar = (function () { 
   
       var playheadHalfSize = 8, // must be half width of playhead defined in CSS 
           containerElm = null, 
           playheadElm = null, 
           backerElm = null, 
           bufferElm = null, 
           progressElm = null, 
           currentPos = 0, // [0,1] relative to range 
           currentBuffer = 0,// [0,1] relative to range 
           listener = null, 
           isSeeking = false, 
   
            setPositionChangeListener = function (funct) { 
               listener = funct; 
            }, 
   
            getSeekBarBounds = function () { 
              return backerElm.getBoundingClientRect(); 
            }, 
   
            onPositionChange = function (event) { 
                var pos = event.pageX || event.clientX; 
                var bounds = getSeekBarBounds(); 
                // normalize position to seek bounds 
                pos -= bounds.left; 
                var percent = pos / (bounds.right - bounds.left); 
   
                // check bounds 
                 if (percent > 1) percent = 1; 
                 else if (percent < 0) percent = 0; 
   
                 currentPos = percent; 
                 setPosition(percent); 
              }, 
   
                 updatePlayhead = function (time, range) { 
                 if (!isSeeking) { 
                 var pos = convertTimeToRelativePosition(time, range); 
                 setPosition(pos); 
              } 
            }, 
   
               setPosition = function (percent) { 
               // adjust to keep playhead graphic inside container on right side 
               var bounds = getSeekBarBounds(); 
               var pos = percent * (bounds.right - bounds.left); 
   
               progressElm.style.width = (pos).toString() + "px"; 
               playheadElm.style.left = (pos-playheadHalfSize).toString() + "px"; 
   
               currentPos = percent; 
               return percent; 
   
               }, 
   
                updateBufferLevel = function (level, range) { 
                if (!isSeeking) { 
                    var position = convertTimeToRelativePosition(level, range); 
                    setBufferLevel(position); 
                   } 
               }, 
   
                 setBufferLevel = function (percent) { 
                    currentBuffer = percent; 
                    var bounds = getSeekBarBounds(); 
                    var pos = percent * (bounds.right - bounds.left); 
   
                           bufferElm.style.width = pos.toString() + "px"; 
                       }, 
   
                       resetSeekBar = function () { 
                          setPosition(currentPos); 
                          setBufferLevel(currentBuffer); 
                       }, 
   
                       convertTimeToRelativePosition = function (time, range) { 
                          // convert time to a percentage of the duration 
                          var position = (time - range.begin) / range.duration; 
                          if (position > 1) position = 1; 
                          else if (position < 0) position = 0; 
                          return position; 
                       }, 
   
                       unattachEvents = function (e) { 
                         this.removeEventListener('mousemove', onPositionChange); 
                         this.removeEventListener('mouseout', unattachEvents); 
                         this.removeEventListener('mouseup', unattachEvents); 
   
                           this.addEventListener('mouseover', attachEvents); 
                           isSeeking = false; 
                       }, 
   
                       attachEvents = function (e) { 
                          this.addEventListener('mousemove', onPositionChange); 
                          this.addEventListener('mouseout', unattachEvents); 
                          this.addEventListener('mouseup', unattachEvents); 
                          isSeeking = true; 
                          return false; 
                       }; 
   
               return  { 
                   init : function () { 
                     containerElm = document.getElementById("seekbar"); 
                     backerElm = document.getElementById("backer"); 
                     playheadElm = document.getElementById("playhead"); 
                     bufferElm = document.getElementById("buffer"); 
                     progressElm = document.getElementById("progress"); 
   
                     // client seek via scrubbing 
                     containerElm.addEventListener('mousedown', attachEvents); 
   
                     // client seek via single click or 'mouseup' after scrubbing 
                     containerElm.addEventListener('click', function (e) { 
                        if (listener !== null && !player.areControlsDisabledInAd()) { 
                           onPositionChange(e); 
                           // callback to notify of desired seek position 
                           listener.call(this, currentPos); 
                           } 
                       }); 
   
                       // end client seek via scrubbing 
                       document.addEventListener('mouseup', function (e) { 
                           containerElm.removeEventListener('mouseover', attachEvents); 
                       }); 
                   }, 
   
                  /** 
                  * Is the playhead currently being scrubbed. 
                  */ 
                  isSeeking : isSeeking, 
   
                  /** 
                  * Change the position of the playhead. 
                  * @param time - time in seconds to position playhead 
                  * @param range - current playback range 
                  */ 
                  updatePlayhead : updatePlayhead, 
   
                  /** 
                  * Change the position of the buffer range. 
                  * @param time - time in seconds to position head of buffer 
                  * @param range - current playback range 
                  */ 
                  updateBufferLevel : updateBufferLevel, 
   
                  /** 
                  * Set listener which is called when the playhead position changes 
                  * by the user event. Listener is not called when playhead position 
                  * changes via updatePlayhead function. 
                  * @param listener - callback function, passed single position argument 
                  * representing the playhead position in the range [0,1]. 
                  */ 
                  setPositionChangeListener : setPositionChangeListener, 
   
                  /** 
                  * Readjust position levels if seekbar is resized. 
                  * Should be called every time the video window changes size. 
                  */ 
                  readjustSeekBar : resetSeekBar 
               }; 
   
           })(); 
   ```
