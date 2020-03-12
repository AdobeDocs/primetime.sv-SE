---
description: Du kan aktivera eller inaktivera funktionen Lazy Ad Resolving med den befintliga Lazy Ad Loading-mekanismen (Lazy Ad Resolving är aktiverat som standard).
keywords: Lazy;Ad resolving;Ad loading;delayLoading
seo-description: Du kan aktivera eller inaktivera funktionen Lazy Ad Resolving med den befintliga Lazy Ad Loading-mekanismen (Lazy Ad Resolving är aktiverat som standard).
seo-title: Aktivera lat och löst
title: Aktivera lat och löst
uuid: a084ee0b-53af-4600-91f6-d30ccc89699d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Aktivera lat och löst {#enable-lazy-ad-resolving}

Du kan aktivera eller inaktivera funktionen Lazy Ad Resolving med den befintliga Lazy Ad Loading-mekanismen (Lazy Ad Resolving är aktiverat som standard).

Du kan aktivera eller inaktivera Lazy Ad Resolving genom att anropa [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) med `true` eller `false`.

1. Använd de booleska värdena `hasDelayAdLoading` och `setDelayAdLoading` metoderna i `AdvertisingMetadata` för att styra tidpunkten för annonsupplösningen och placeringen av annonser på tidslinjen:

   * Om `hasDelayAdLoading` returnerar false väntar TVSDK tills alla annonser är lösta och placerade innan övergången till tillståndet PREPARED görs.
   * Om `hasDelayAdLoading` returnerar true tolkar TVSDK bara de initiala annonserna och övergångarna till tillståndet PREPARED. De återstående annonserna löses och placeras under uppspelningen.
   * När `hasPreroll` eller `hasLivePreroll` returnerar false antar TVSDK att det inte finns någon förhandsgranskning och startar uppspelningen av innehållet omedelbart. Standardvärdet är true.

      API:er som är relevanta för lata annonsupplösningar:

      ```
      Class: 
         com.adobe.mediacore.metadata.AdvertisingMetadata 
      
      Methods: 
      […] 
          public final boolean hasDelayAdLoading() // Check if Lazy Ad Resolving enabled 
          public final void setDelayAdLoading()    // Enable or disable Lazy Ad Resolving 
          public final boolean hasPreroll()        // Check for existence of pre-roll ads 
          public final void setPreroll()           // Set pre-roll true or false 
          public final boolean hasLivePreroll()    // Check for live pre-roll ads 
          public final void setLivePreroll()       // Set live pre-roll true or false 
      […]
      ```

1. Om du exakt vill spegla annonser som tips i ett navigeringsfält lyssnar du efter händelsen och ritar om navigeringsfältet varje gång du får den här händelsen. `TimelineEvent`

   När Lazy Ad Resolving är aktiverat för VOD-strömmar placeras inte alla annonser på tidslinjen när spelaren försätts i tillståndet PREPARED, så spelaren måste rita om rensningsfältet explicit.

   TVSDK optimerar utskicket av den här händelsen för att minimera antalet gånger som du måste rita om rensningsfältet. Därför är antalet tidslinjehändelser inte relaterat till antalet annonsbrytningar som ska placeras på tidslinjen. Om du till exempel har fem annonsbrytningar kanske du inte får exakt fem händelser.

   ```java
   mediaPlayer.addEventListener 
       (MediaPlayerEvent.TIMELINE_UPDATED, timelineUpdatedEventListener); 
   /** 
    * ... 
    */ 
   public void onTimelineUpdated(TimelineEvent event) { 
   
       for (PlaybackManagerEventListener listener : eventListeners) { 
           listener.onUpdate(getLocalSeekRange(), event.getTimeline()); 
       } 
   } 
   ```

>Om du vill verifiera om funktionen Lazy Ad Resolving är aktiverad eller inaktiverad ringer du `AdvertisingMetadata.hasDelayAdLoading`. Returvärdet är `true` att Lazy Ad Resolving är aktiverat. `false` betyder att funktionen är inaktiverad.

