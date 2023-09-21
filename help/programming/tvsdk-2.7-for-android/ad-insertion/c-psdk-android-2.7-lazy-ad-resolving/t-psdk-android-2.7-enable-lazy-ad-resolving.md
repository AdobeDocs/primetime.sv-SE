---
description: Du kan aktivera eller inaktivera funktionen Lazy Ad Resolving med den befintliga Lazy Ad Loading-mekanismen (Lazy Ad Resolving är aktiverat som standard).
keywords: Lazy;Annonsupplösning;Annonsinläsning;delayLoading
title: Aktivera lat och löst
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Aktivera lat och löst {#enable-lazy-ad-resolving}

Du kan aktivera eller inaktivera funktionen Lazy Ad Resolving med den befintliga Lazy Ad Loading-mekanismen (Lazy Ad Resolving är aktiverat som standard).

Du kan aktivera eller inaktivera Lazy Ad Resolving genom att ringa [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) med `true` eller `false`.

1. Använda det booleska värdet `hasDelayAdLoading` och `setDelayAdLoading` metoder i `AdvertisingMetadata` för att styra timing för annonsupplösning och placering av annonser på tidslinjen:

   * If `hasDelayAdLoading` returnerar false, TVSDK väntar tills alla annonser är lösta och placerade innan övergången till tillståndet PREPARED görs.
   * If `hasDelayAdLoading` returnerar true, tolkar TVSDK bara de initiala annonserna och övergångarna till tillståndet PREPARED. De återstående annonserna löses och placeras under uppspelningen.
   * När `hasPreroll` eller `hasLivePreroll` return false, TVSDK antar att det inte finns någon förhandsgranskning och startar uppspelningen av innehållet omedelbart. Standardvärdet är true.

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

1. Lyssna efter `TimelineEvent` och rita om rensningsfältet varje gång du får den här händelsen.

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

>För att verifiera om funktionen Lazy Ad Resolving är aktiverad eller inaktiverad, ring `AdvertisingMetadata.hasDelayAdLoading`. Ett returvärde för `true` Lazy Ad Resolving är aktiverat. `false` betyder att funktionen är inaktiverad.
