---
description: Du kan aktivera eller inaktivera funktionen Lazy Ad Resolving med den befintliga Lazy Ad Loading-mekanismen (Lazy Ad Resolving är inaktiverat som standard).
keywords: Lazy;Ad resolving;Ad loading;delayLoading
seo-description: Du kan aktivera eller inaktivera funktionen Lazy Ad Resolving med den befintliga Lazy Ad Loading-mekanismen (Lazy Ad Resolving är inaktiverat som standard).
seo-title: Aktivera lat och löst
title: Aktivera lat och löst
uuid: 91884eea-a622-4f5d-b6a8-36bb0050ba1d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Aktivera lat och löst {#enable-lazy-ad-resolving}

Du kan aktivera eller inaktivera funktionen Lazy Ad Resolving med den befintliga Lazy Ad Loading-mekanismen (Lazy Ad Resolving är inaktiverat som standard).

Du kan aktivera eller inaktivera Lazy Ad Resolving genom att anropa [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) med true eller false.

* Använd metoderna Boolean *hasDelayAdLoading* och *setDelayAdLoading* i AdvertisingMetadata för att styra timing för annonsupplösning och placering av annonser på tidslinjen:

   * Om *hasDelayAdLoading* returnerar false väntar TVSDK tills alla annonser har lösts och placerats innan övergången till tillståndet PREPARED görs.
   * Om *hasDelayAdLoading* returnerar true tolkas bara de initiala annonserna och övergångarna till tillståndet PREPARED.

      * De återstående annonserna löses och placeras under uppspelningen.
   * När *hasPreroll *eller *hasLivePreroll* returnerar false antar TVSDK att det inte finns någon förhandsgranskning och att uppspelningen av innehållet startar omedelbart. Dessa är som standard inställda på true.


**API:er som är relevanta för lata annonsupplösningar:**

```
Class:    com.adobe.mediacore.metadata.AdvertisingMetadata 
Methods: 
    public final boolean hasDelayAdLoading() // Check if Lazy Ad Resolving enabled 
    public final void setDelayAdLoading() // Enable or disable Lazy Ad Resolving 
    public final void setDelayAdLoadingTolerance() // Sets the Lazy Ad Resolving Tolerance level.  This value is added to the BufferControlParameters::playBufferTime and the content's EXT-X-TARGETDURATION to determine when ad breaks should resolve 
    public final double getDelayAdLoadingTolerance() // Gets the Lazy Ad Resolving Tolerance level 
    public final boolean hasPreroll() // Check for existence of pre-roll ads 
    public final void setPreroll() // Set pre-roll true or false 
    public final boolean hasLivePreroll() // Check for live pre-roll ads 
    public final void setLivePreroll() // Set live pre-roll true or false

Class:     com.adobe.mediacore.timeline.TimelineMarker 
Methods: 
    public double getDuration() // Returns the current duration of the TimelineMarker.  This will be zero if the ad break has not yet resolved. 
    public Placement.Type getPlacementType() // Returns whether
```

Om du exakt vill spegla annonser som tips i ett navigeringsfält lyssnar du efter `TimelineEvent`händelsen och ritar om navigeringsfältet varje gång du får den här händelsen.

När Lazy Ad Resolving är aktiverat för VOD-strömmar placeras alla annonsbrytningar på tidslinjen, men många av annonsbrytningarna kommer inte att åtgärdas än. Programmet kan avgöra om markörerna ska ritas eller inte genom att kontrollera `TimelineMarker::getDuration()`. Om värdet är större än noll har annonserna inom annonsbrytningen lösts.

TVSDK skickar den här händelsen när en annonsbrytning har lösts, och även när spelaren övergår till statusen PREPARED.

```
mediaPlayer.addEventListener(MediaPlayerEvent.TIMELINE_UPDATED, timelineUpdatedEventListener); 
/** 
* ... 
*/ 
public void onTimelineUpdated(TimelineEvent event) { 
for (PlaybackManagerEventListener listener : eventListeners) { 
  listener.onUpdate(getLocalSeekRange(), event.getTimeline()); 
}
```
