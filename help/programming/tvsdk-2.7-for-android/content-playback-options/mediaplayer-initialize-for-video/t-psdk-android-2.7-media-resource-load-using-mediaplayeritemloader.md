---
description: Med MediaPlayerItemLoader kan du få information om en medieström utan att initiera en MediaPlayer-instans. Detta är särskilt användbart i pre-buffring av strömmar så att uppspelningen kan börja utan fördröjning.
seo-description: Med MediaPlayerItemLoader kan du få information om en medieström utan att initiera en MediaPlayer-instans. Detta är särskilt användbart i pre-buffring av strömmar så att uppspelningen kan börja utan fördröjning.
seo-title: Läsa in en medieresurs med MediaPlayerItemLoader
title: Läsa in en medieresurs med MediaPlayerItemLoader
uuid: 43ca2470-1fd2-4f66-94fe-a12ed17b52d7
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# Läsa in en medieresurs med MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

Med MediaPlayerItemLoader kan du få information om en medieström utan att initiera en MediaPlayer-instans. Detta är särskilt användbart i pre-buffring av strömmar så att uppspelningen kan börja utan fördröjning.

Klassen hjälper dig att byta ut en medieresurs för den aktuella `MediaPlayerItemLoader` utan att bifoga en vy till en `MediaPlayerItem` `MediaPlayer` instans, vilket allokerar maskinvaruresurser för videoavkodning. Ytterligare steg krävs för DRM-skyddat innehåll, men de beskrivs inte i den här handboken.

>[!IMPORTANT]
>
>TVSDK stöder inte en enda `QoSProvider` åtgärd för både `itemLoader` och `MediaPlayer`. Om programmet använder Instant On måste programmet behålla två `QoS` instanser och hantera båda instanserna för informationen. Mer information finns [i Snabbstart](../../content-playback-options/buffering-configuration/c-psdk-android-2.7-instant-on.md) .

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
   >Skapa en separat instans av `MediaPlayerItemLoader` för varje resurs. Använd inte en `MediaPlayerItemLoader` instans för att läsa in flera resurser.

1. Implementera den klass som `ItemLoaderListener` ska ta emot meddelanden från `MediaPlayerItemLoader` instansen.

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

   Gör något av följande i återanropet: `onLoadComplete()`

   * Kontrollera att allt som kan påverka buffringen, till exempel när du väljer WebVTT eller ljudspår, är klart och anropar `prepareBuffer()` för att utnyttja direktuppspelningen.
   * Bifoga objektet till `MediaPlayer` instansen med `replaceCurrentItem()`.
   Om du anropar `prepareBuffer()`får du händelsen BUFFER_PREPARED i din `onBufferPrepared` hanterare när förberedelsen är klar.

1. Anropa `load` instansen och skicka den resurs som ska läsas in, och eventuellt innehålls-ID:t och en `MediaPlayerItemLoader` `MediaPlayerItemConfig` instans.

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. Om du vill buffra från en annan punkt än direktuppspelningens början anropar du `prepareBuffer()` med den position (i millisekunder) där buffringen ska börja.
1. Använd metoderna `replaceCurrentItem()` och `play()` för `MediaPlayer` att börja spela upp från den punkten.
1. Vänta på inaktiv status och ring `replaceCurrentItem`.
1. Spela upp objektet.

   * Om objektet har lästs in men inte buffrats:

      1. Vänta på initierad status.
      1. Ring `prepareToPlay()`.
      1. Vänta på statusen FÖRBEREDD.
      1. Ring `play()`.
   * Om objektet är buffrat:

      1. Vänta på den buffertförberedda händelsen.
      1. Ring `play()`.