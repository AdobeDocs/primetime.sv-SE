---
description: Om du aktiverar direkt innebär det att en eller flera kanaler är förinlästa. När användare väljer en kanal eller byter kanal spelas innehållet upp omedelbart. Bufferten är klar när användaren börjar titta.
title: Direkt på
exl-id: a9c0b9d0-ef2b-4113-bd08-e2b2792b04fb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Direkt på {#instant-on}

Om du aktiverar direkt innebär det att en eller flera kanaler är förinlästa. När användare väljer en kanal eller byter kanal spelas innehållet upp omedelbart. Bufferten är klar när användaren börjar titta.

Utan Instant On initierar TVSDK mediet som ska spelas upp, men börjar inte buffra strömmen förrän programmet anropar `play`. Användaren ser inget innehåll förrän bufferten är klar. Med Instant On kan du starta flera mediespelarinstanser (eller inläsare för mediespelare) och TVSDK börjar buffra strömmarna direkt. När en användare ändrar kanalen och strömmen har buffrats korrekt anropas `play` i den nya kanalen startar uppspelningen omedelbart.

Även om det inte finns några begränsningar för antalet `MediaPlayer` och `MediaPlayerItemLoader` instanser som TVSDK kan köra och fler instanser kräver mer resurser. Programmets prestanda kan påverkas av antalet instanser som körs. Mer information om `MediaPlayerItemLoader`, se [Läsa in en medieresurs i mediespelaren](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md).

>[!IMPORTANT]
>
>TVSDK stöder inte en enda `QoSProvider` att arbeta med båda `itemLoader` och `MediaPlayer`. Om kunden använder Instant On måste programmet underhålla två QoS-instanser och hantera båda instanserna för informationen.

Mer information om `MediaPlayerItemLoader`, se [Läsa in en medieresurs med MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md).

## Lägga till en QoS-providerinstans i mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* Skapa och bifoga en QoS-provider till en `mediaPlayerItemLoader` instance

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   När uppspelningen har startat använder du `_qosProvider` för att `timeToLoad` och `timeToPrepare` QoSdata. Återstående QoS-mått kan hämtas med `QoSProvider` som är kopplad till `mediaPlayer`.

   Mer information om `MediaPlayerItemLoader`, se [Läsa in en medieresurs med MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md#use-mediaplayeritemloader).

## Konfigurera buffring för Direkt på {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK innehåller metoder och statusar som gör att du kan använda Direktaktivering med en medieresurs.

>[!NOTE]
>
>Adobe rekommenderar att du använder `MediaPlayerItemLoader` för InstantOn. Används `MediaPlayerItemLoader`i stället för `MediaPlayer`, se media-resource-load-using-mediaplayeritemloader .

1. Bekräfta att resursen har lästs in och att spelaren är redo att spela upp resursen.
1. Före anrop `play`, ring `prepareBuffer` för varje `MediaPlayer` -instans.

   >[!NOTE]
   >
   >`prepareBuffer` aktiverar Instant On, och TVSDK börjar buffra omedelbart och skickar `BUFFERING_COMPLETED` -händelsen när bufferten är full.

   >[!TIP]
   >
   >Som standard `prepareBuffer` och `prepareToPlay` konfigurera medieströmmen så att den börjar spelas upp från början. Om du vill börja vid en annan position skickar du positionen (i millisekunder) till `prepareToPlay`.

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

1. När du får `BUFFERING_COMPLETE` börjar du spela upp objektet eller visar visuell feedback som anger att innehållet är helt buffrat.

   >[!NOTE]
   >
   >Om du ringer `play`ska uppspelningen börja omedelbart.
