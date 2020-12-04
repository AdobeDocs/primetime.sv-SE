---
description: Från det att MediaPlayer-instansen skapas tills den avslutas övergår den här instansen från ett läge till nästa.
seo-description: Från det att MediaPlayer-instansen skapas tills den avslutas övergår den här instansen från ett läge till nästa.
seo-title: Livscykel och lägen för MediaPlayer-objektet
title: Livscykel och lägen för MediaPlayer-objektet
uuid: fe76ea80-aaa8-43bc-9b81-85e0551f70dd
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---


# Livscykel och lägen för MediaPlayer-objektet{#life-cycle-and-states-of-the-mediaplayer-object}

Från det att MediaPlayer-instansen skapas tills den avslutas övergår den här instansen från ett läge till nästa.

Här är möjliga lägen:

* **IDLE**:  `MediaPlayerStatus.IDLE`

* **INITIERAR**:  `MediaPlayerStatus.INITIALIZING`

* **INITIERAT**:  `MediaPlayerStatus.INITIALIZED`

* **FÖRBEREDER**:  `MediaPlayerStatus.PREPARING`

* **FÖRBEREDD**:  `MediaPlayerStatus.PREPARED`

* **SPELA UPP**:  `MediaPlayerStatus.PLAYING`

* **PAUSAT**:  `MediaPlayerStatus.PAUSED`

* **SÖKER**:  `MediaPlayerStatus.SEEKING`

* **FULLSTÄNDIGT**:  `MediaPlayerStatus.COMPLETE`

* **FEL**:  `MediaPlayerStatus.ERROR`

* **SLÄPPT**:  `MediaPlayerStatus.RELEASED`

Den fullständiga listan med lägen definieras i `MediaPlayerStatus`.

Att känna till spelarens tillstånd är användbart eftersom vissa åtgärder bara är tillåtna när spelaren är i ett visst läge. Det går till exempel inte att anropa `play` i IDLE-läge. Den måste anropas efter att ha nått PREPARED-tillståndet. FELläget ändrar också vad som kan hända härnäst.

När en medieresurs läses in och spelas upp, övergår spelaren på följande sätt:

1. Det inledande tillståndet är IDLE.
1. Programmet anropar `MediaPlayer.replaceCurrentResource`, vilket flyttar spelaren till INITIALIZING-läget.
1. Om webbläsar-TVSDK läser in resursen ändras läget till INITIALIZED.
1. Programmet anropar `MediaPlayer.prepareToPlay` och läget ändras till PREPARING.
1. Webbläsare-TVSDK förbereder medieströmmen och startar annonslösningen och annonsinfogningen (om den är aktiverad).

   När det här steget är klart infogas annonser i tidslinjen eller så har annonsproceduren misslyckats och spelarläget ändras till PREPARED.
1. När programmet spelar upp och pausar media flyttas läget mellan PLAYING och PAUSED.

   >[!TIP]
   >
   >När du navigerar bort från uppspelningen, stänger av enheten eller växlar program ändras läget till SUSPENDED och resurser frigörs när du spelar upp eller pausar. Återställ mediespelaren för att fortsätta.

1. När spelaren når slutet av strömmen blir läget SLUTFÖRD.
1. När programmet släpper mediespelaren ändras läget till FRISLÄPPT.
1. Om ett fel inträffar under processen ändras statusen till FEL.

Här följer en illustration av livscykeln för en MediaPlayer-instans:

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

Du kan använda läget för att ge användaren feedback om processen (till exempel en snurra som väntar på nästa lägesändring) eller för att utföra nästa steg i uppspelningen av media, till exempel vänta på rätt läge innan du anropar nästa metod.

Exempel:

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

