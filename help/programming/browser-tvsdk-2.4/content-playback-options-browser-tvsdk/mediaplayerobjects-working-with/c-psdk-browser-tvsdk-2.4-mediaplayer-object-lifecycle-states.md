---
description: Från det att MediaPlayer-instansen skapas tills den avslutas övergår den här instansen från ett läge till nästa.
title: Livscykel och lägen för MediaPlayer-objektet
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# Livscykel och lägen för MediaPlayer-objektet{#life-cycle-and-states-of-the-mediaplayer-object}

Från det att MediaPlayer-instansen skapas tills den avslutas övergår den här instansen från ett läge till nästa.

Här är möjliga lägen:

* **IDLE**: `MediaPlayerStatus.IDLE`

* **INITIERAR**: `MediaPlayerStatus.INITIALIZING`

* **INITIERAD**: `MediaPlayerStatus.INITIALIZED`

* **FÖRBEREDER**: `MediaPlayerStatus.PREPARING`

* **FÖRBEREDD**: `MediaPlayerStatus.PREPARED`

* **SPELAR**: `MediaPlayerStatus.PLAYING`

* **PAUSAT**: `MediaPlayerStatus.PAUSED`

* **SÖKER**: `MediaPlayerStatus.SEEKING`

* **SLUTFÖRD**: `MediaPlayerStatus.COMPLETE`

* **FEL**: `MediaPlayerStatus.ERROR`

* **SLÄPPT**: `MediaPlayerStatus.RELEASED`

Den fullständiga listan med lägen definieras i `MediaPlayerStatus`.

Att känna till spelarens tillstånd är användbart eftersom vissa åtgärder bara är tillåtna när spelaren är i ett visst läge. Till exempel: `play` kan inte anropas i IDLE-läge. Den måste anropas efter att ha nått PREPARED-tillståndet. FELläget ändrar också vad som kan hända härnäst.

När en medieresurs läses in och spelas upp, övergår spelaren på följande sätt:

1. Det inledande tillståndet är IDLE.
1. Dina programsamtal `MediaPlayer.replaceCurrentResource`, som flyttar spelaren till INITIALIZING-läget.
1. Om webbläsar-TVSDK läser in resursen ändras läget till INITIALIZED.
1. Dina programsamtal `MediaPlayer.prepareToPlay`och läget ändras till FÖRBEREDELSE.
1. Webbläsare-TVSDK förbereder medieströmmen och startar annonslösningen och annonsinfogningen (om den är aktiverad).

   När det här steget är klart infogas annonser i tidslinjen eller så har annonsproceduren misslyckats och spelarläget ändras till PREPARED.
1. När programmet spelar upp och pausar media flyttas läget mellan PLAYING och PAUSED.

   >[!TIP]
   >
   >När du navigerar bort från uppspelningen, stänger av enheten eller växlar program ändras läget till SUSPENDED och resurser frigörs när du spelar upp eller pausar. Återställ mediespelaren om du vill fortsätta.

1. När spelaren kommer till slutet av strömmen blir läget SLUTFÖRD.
1. När programmet släpper mediespelaren ändras läget till FRISLÄPPT.
1. Om ett fel inträffar under processen ändras statusen till FEL.

Här följer en illustration av livscykeln för en MediaPlayer-instans:

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

Du kan använda läget för att ge användaren feedback om processen (till exempel en snurra som väntar på nästa lägesändring) eller för att utföra nästa steg i uppspelningen av media, till exempel vänta på rätt läge innan du anropar nästa metod.

Till exempel:

```js
function onStateChanged(state) { 
    switch(state) { 
        // It is recommended that you call prepareToPlay()  
        // after receiving the INITIALIZED state             
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            mediaPlayer.prepareToPlay(); 
            break; 
    } 
} 
```
