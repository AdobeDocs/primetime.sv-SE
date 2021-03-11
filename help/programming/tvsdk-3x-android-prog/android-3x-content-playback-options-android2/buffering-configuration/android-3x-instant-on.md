---
description: Om du aktiverar direkt innebär det att en eller flera kanaler är förinlästa. När användare väljer en kanal eller byter kanal spelas innehållet upp omedelbart. Bufferten är klar när användaren börjar titta.
title: Direkt på
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Direkt på {#instant-on}

Om du aktiverar direkt innebär det att en eller flera kanaler är förinlästa. När användare väljer en kanal eller byter kanal spelas innehållet upp omedelbart. Bufferten är klar när användaren börjar titta.

Utan Instant On initierar TVSDK mediet som ska spelas upp, men börjar inte buffra strömmen förrän programmet anropar `play`. Användaren ser inget innehåll förrän bufferten är klar. Med Instant On kan du starta flera mediespelarinstanser (eller inläsare för mediespelare) och TVSDK börjar buffra strömmarna direkt. När en användare ändrar kanalen och strömmen har buffrats korrekt startar ett anrop till `play` på den nya kanalen uppspelningen omedelbart.

Även om det inte finns några gränser för hur många instanser av `MediaPlayer` och `MediaPlayerItemLoader` som TVSDK kan köra, kräver körningen av fler instanser mer resurser. Programmets prestanda kan påverkas av antalet instanser som körs. Mer information om `MediaPlayerItemLoader` finns i [Läs in en medieresurs i mediespelaren](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md).

>[!IMPORTANT]
>
>TVSDK stöder inte en enskild `QoSProvider`-instans för att arbeta med både `itemLoader` och `MediaPlayer`. Om kunden använder Instant On måste programmet underhålla två QoS-instanser och hantera båda instanserna för informationen.

Mer information om `MediaPlayerItemLoader` finns i [Läs in en medieresurs med MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Lägg till en QoS-providerinstans i mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* Skapa och koppla en QoS-provider till en `mediaPlayerItemLoader`-instans

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   När uppspelningen startar använder du `_qosProvider` för att hämta `timeToLoad` och `timeToPrepare` QoSdata. Återstående QoS-mått kan hämtas med `QoSProvider` som är kopplad till `mediaPlayer`.

   Mer information om `MediaPlayerItemLoader` finns i [Läs in en medieresurs med MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Konfigurera buffring för Instant On {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK innehåller metoder och statusar som gör att du kan använda Direktaktivering med en medieresurs.

>[!NOTE]
>
>Adobe rekommenderar att du använder `MediaPlayerItemLoader` för InstantOn. Mer information om hur du använder `MediaPlayerItemLoader` i stället för `MediaPlayer` finns i [Läs in en medieresurs med MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

1. Bekräfta att resursen har lästs in och att spelaren är redo att spela upp resursen.
1. Innan du anropar `play` ska du ringa `prepareBuffer` för varje `MediaPlayer`-instans.

   `prepareBuffer` aktiverar Instant On och TVSDK börjar buffra omedelbart och skickar  `BUFFERING_COMPLETED` händelsen när bufferten är full.

   >[!TIP]
   >
   >Som standard konfigurerar `prepareBuffer` och `prepareToPlay` medieströmmen så att den börjar spelas upp från början. Om du vill börja på en annan position skickar du positionen (i millisekunder) till `prepareToPlay`.

   ```
   @Override 
   public void onStatusChanged(MediaPlayerStatus status) { 
       switch (status) { 
           case INITIALIZED: 
               // This example starts 5 seconds into the stream. 
               mediaPlayer.prepareToPlay(5000); 
               break; 
           case PREPARING: 
               break; 
           case PREPARED: 
               mediaPlayer.prepareBuffer(); 
               break; 
           ... 
       } 
   }
   ```

1. När du tar emot händelsen `BUFFERING_COMPLETE` börjar du spela upp objektet eller visar visuell feedback som anger att innehållet är helt buffrat.

   >[!NOTE]
   >
   >Om du anropar `play` ska uppspelningen börja omedelbart.