---
description: Med MediaPlayerItemLoader kan du få information om en medieström utan att initiera en MediaPlayer-instans. Detta är särskilt användbart i pre-buffring av strömmar så att uppspelningen kan börja utan fördröjning.
title: Läsa in en medieresurs med MediaPlayerItemLoader
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Läsa in en medieresurs med MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

Med MediaPlayerItemLoader kan du få information om en medieström utan att initiera en MediaPlayer-instans. Detta är särskilt användbart i pre-buffring av strömmar så att uppspelningen kan börja utan fördröjning.

The `MediaPlayerItemLoader` klassen hjälper dig att byta ut en medieresurs för den aktuella `MediaPlayerItem` utan att bifoga en vy till en `MediaPlayer` -instans, som allokerar maskinvaruresurser för videoavkodning. Ytterligare steg krävs för DRM-skyddat innehåll, men de beskrivs inte i den här handboken.

>[!IMPORTANT]
>
>TVSDK stöder inte en enda `QoSProvider` att arbeta med båda `itemLoader` och `MediaPlayer`. Om programmet använder Instant On måste programmet underhålla två `QoS` -instanser och hantera båda instanserna för informationen. Se  [direkt](../../content-playback-options/buffering-configuration/c-psdk-android-2.7-instant-on.md) för mer information.

1. Skapa en instans av `MediaPlayerItemLoader`.

   ```java
   private MediaPlayerItemLoader createLoader() { 
       MediaPlayerItemLoader itemLoader =   
         new MediaPlayerItemLoader(this, new MediaPlayerItemLoader.LoaderListener() { 
           public void onError(PSDKErrorCode mediaErrorCode, String description) { 
               //Do something 
           } 
   
           public void onLoadComplete(MediaPlayerItem playerItem) { 
               loader.prepareBuffer(); 
           } 
   
           public void onBufferingBegin() { 
               //Do something 
           } 
   
           public void onBufferPrepared() { 
               mPlayer.reset(); 
           }  
       }); 
   
       itemLoader.setKeepRebufferingForLive(true); 
       return itemLoader; 
   } 
   ```

   >[!TIP]
   >
   >Skapa en separat instans av `MediaPlayerItemLoader` för varje resurs. Använd inte en `MediaPlayerItemLoader` -instans för att läsa in flera resurser.

1. Implementera `ItemLoaderListener` klassen som ska ta emot meddelanden från `MediaPlayerItemLoader` -instans.

   ```java
   private MediaPlayerItemLoader createLoader() { 
       MediaPlayerItemLoader itemLoader =   
         new MediaPlayerItemLoader(this, new MediaPlayerItemLoader.LoaderListener() { 
           public void onError(PSDKErrorCode mediaErrorCode, String description) { 
               //Do something 
           } 
           public void onLoadComplete(MediaPlayerItem playerItem) { 
               loader.prepareBuffer(); 
           } 
           public void onBufferingBegin() { 
               //Do something 
           } 
           public void onBufferPrepared() { 
               mPlayer.reset(); 
           }  
       } ); 
   
       itemLoader.setKeepRebufferingForLive(true); 
       return itemLoader; 
   }
   ```

   I `onLoadComplete()` återanrop gör du något av följande:

   * Kontrollera att allt som kan påverka buffringen, till exempel när du väljer WebVTT eller ljudspår, är fullständigt och att anropa `prepareBuffer()` för att utnyttja möjligheterna direkt.
   * Bifoga objektet till `MediaPlayer` instans genom att använda `replaceCurrentItem()`.

   Om du ringer `prepareBuffer()`får du händelsen BUFFER_PREPARED i `onBufferPrepared` hanterare när preparatet är klart.

1. Utlysning `load` på `MediaPlayerItemLoader` instansen och skicka resursen som ska läsas in, och eventuellt innehålls-ID:t, och `MediaPlayerItemConfig` -instans.

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. Om du vill buffra från en annan punkt än strömmens början anropar du `prepareBuffer()` med den position (i millisekunder) där buffringen ska börja.
1. Använd `replaceCurrentItem()` och `play()` metoder `MediaPlayer` för att börja spela från den punkten.
1. Vänta på inaktiv status och samtal `replaceCurrentItem`.
1. Spela upp objektet.

   * Om objektet har lästs in men inte buffrats:

      1. Vänta på initierad status.
      1. Utlysning `prepareToPlay()`.
      1. Vänta på statusen FÖRBEREDD.
      1. Utlysning `play()`.

   * Om objektet är buffrat:

      1. Vänta på den buffertförberedda händelsen.
      1. Utlysning `play()`.
