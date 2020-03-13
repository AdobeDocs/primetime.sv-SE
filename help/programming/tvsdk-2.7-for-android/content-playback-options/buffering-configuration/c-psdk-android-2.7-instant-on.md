---
description: Om du aktiverar direkt innebär det att en eller flera kanaler är förinlästa. När användare väljer en kanal eller byter kanal spelas innehållet upp omedelbart. Bufferten är klar när användaren börjar titta.
seo-description: Om du aktiverar direkt innebär det att en eller flera kanaler är förinlästa. När användare väljer en kanal eller byter kanal spelas innehållet upp omedelbart. Bufferten är klar när användaren börjar titta.
seo-title: Direkt på
title: Direkt på
uuid: 7e14b779-2a36-4ff4-a365-9ac49a836ff3
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184

---


# Direkt på {#instant-on}

Om du aktiverar direkt innebär det att en eller flera kanaler är förinlästa. När användare väljer en kanal eller byter kanal spelas innehållet upp omedelbart. Bufferten är klar när användaren börjar titta.

Utan Instant On initierar TVSDK mediet som ska spelas upp, men börjar inte buffra strömmen förrän programmet anropar `play`. Användaren ser inget innehåll förrän bufferten är klar. Med Instant On kan du starta flera mediespelarinstanser (eller inläsare för mediespelare) och TVSDK börjar buffra strömmarna direkt. När en användare ändrar kanalen och strömmen har buffrats korrekt startar uppspelningen omedelbart om den nya kanalen anropas `play` .

Även om det inte finns några gränser för hur många `MediaPlayer` och `MediaPlayerItemLoader` många instanser TVSDK kan köras kräver körning av fler instanser mer resurser. Programmets prestanda kan påverkas av antalet instanser som körs. Mer information om `MediaPlayerItemLoader`finns i [Läsa in en medieresurs i mediespelaren](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md).

>[!IMPORTANT]
>
>TVSDK stöder inte en enda `QoSProvider` åtgärd för både `itemLoader` och `MediaPlayer`. Om kunden använder Instant On måste programmet underhålla två QoS-instanser och hantera båda instanserna för informationen.

Mer information om `MediaPlayerItemLoader`finns i [Läsa in en medieresurs med MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md).

## Lägga till en QoS-providerinstans i mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* Skapa och koppla en QoS-provider till en `mediaPlayerItemLoader` instans

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   När uppspelningen startar använder du `_qosProvider` för att hämta `timeToLoad` och `timeToPrepare` QoSdata. Återstående QoS-mått kan hämtas med hjälp av de `QoSProvider` som är kopplade till `mediaPlayer`.

   Mer information om `MediaPlayerItemLoader`finns i [Läsa in en medieresurs med MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md#use-mediaplayeritemloader).

## Konfigurera buffring för Direkt på {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK innehåller metoder och statusar som gör att du kan använda Direktaktivering med en medieresurs.

>[!NOTE]
>
>Adobe rekommenderar att du använder `MediaPlayerItemLoader` för InstantOn. Mer information `MediaPlayerItemLoader`finns i media-resource-load-using-mediaplayeritemloader i stället `MediaPlayer`för .

1. Bekräfta att resursen har lästs in och att spelaren är redo att spela upp resursen.
1. Innan du anropar `play`anropar du `prepareBuffer` för varje `MediaPlayer` instans.

   >[!NOTE]
   >
   >`prepareBuffer` aktiverar Instant On och TVSDK börjar buffra omedelbart och skickar `BUFFERING_COMPLETED` händelsen när bufferten är full.

   >[!TIP]
   >
   >Som standard `prepareBuffer` och `prepareToPlay` ställer in medieströmmen så att den börjar spelas upp från början. Om du vill börja vid en annan position skickar du positionen (i millisekunder) till `prepareToPlay`.

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

1. När du tar emot `BUFFERING_COMPLETE` händelsen börjar du spela upp objektet eller visar visuell feedback som anger att innehållet är helt buffrat.

   >[!NOTE]
   >
   >Om du anropar `play`ska uppspelningen börja omedelbart.

