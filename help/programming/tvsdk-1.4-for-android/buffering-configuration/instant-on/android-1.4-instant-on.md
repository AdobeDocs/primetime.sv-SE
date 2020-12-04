---
description: Med termen Direkt on avses att förhandsladda en eller flera kanaler så att en användare som väljer en kanal eller byter kanal ser innehållet spelas upp direkt. Bufferten görs redan när användaren börjar titta.
seo-description: Med termen Direkt on avses att förhandsladda en eller flera kanaler så att en användare som väljer en kanal eller byter kanal ser innehållet spelas upp direkt. Bufferten görs redan när användaren börjar titta.
seo-title: Direkt på
title: Direkt på
uuid: 4cb4d221-170f-46e8-af26-32f259377617
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Direkt på {#instant-on}

Med termen Direkt on avses att förhandsladda en eller flera kanaler så att en användare som väljer en kanal eller byter kanal ser innehållet spelas upp direkt. Bufferten görs redan när användaren börjar titta.

Utan direktaktivering initierar TVSDK mediet som ska spelas upp, men börjar inte buffra strömmen förrän programmet anropar `play`. Användaren ser inget innehåll förrän bufferten är klar. Med direktaktivering kan du starta flera mediespelarinstanser (eller inläsare för mediespelare) och TVSDK börjar buffra strömmarna direkt.

När en användare ändrar kanalen och strömmen har buffrats korrekt startar ett anrop till `play` på den nya kanalen uppspelningen omedelbart.

Även om det inte finns några gränser för hur många `MediaPlayer`-instanser TVSDK kan köras, kräver körning av fler instanser mer resurser. Programmets prestanda kan påverkas av antalet instanser som körs. Mer information om de här instanserna finns i [Läsa in en medieresurs med MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).

## Konfigurera buffring för direktuppspelning {#configure-buffering-for-instant-on-playback}

Med direktstart kan användare växla kanaler och uppspelningen startar omedelbart utan väntetid. När du aktiverar direkt buffrar TVSDK en eller flera kanaler innan uppspelningen börjar.

1. Bekräfta att resursen har lästs in och är klar för uppspelning genom att bekräfta att statusen är FÖRBEREDD.
1. Innan du anropar `play` ska du ringa `prepareBuffer` för varje `MediaPlayer`-instans.

   Detta aktiverar direkt, vilket innebär att TVSDK börjar buffra utan att spela upp medieresursen. TVSDK skickar händelsen `BUFFERING_COMPLETED` när bufferten är full.

   >[!NOTE]
   >
   >Som standard konfigurerar `prepareBuffer` och `prepareToPlay` medieströmmen så att den börjar spelas upp från början. Om du vill börja på en annan position skickar du positionen (i millisekunder) till `prepareToPlay`.

   ```java
   @Override 
   public void onStateChanged(MediaPlayer.PlayerState state,  
                              MediaPlayerNotification notification) { 
       switch (state) { 
           case INITIALIZED: 
               // By default, prepareToPlay and prepareBuffer buffer and start playing 
               // from the beginning of the stream. To start at another position, 
               // pass it into prepareToPlay. This example starts 5 seconds into the stream. 
               _mediaPlayer.prepareToPlay(5000); 
               break; 
           case PREPARING: 
               break; 
           case PREPARED: 
               _mediaPlayer.prepareBuffer(); 
               break; 
           ... 
       } 
   }
   ```

1. När du tar emot händelsen `BUFFERING_COMPLETE` börjar du spela upp objektet eller visar visuell feedback som anger att innehållet är helt buffrat.

   Om du anropar `play` ska uppspelningen börja omedelbart.

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
