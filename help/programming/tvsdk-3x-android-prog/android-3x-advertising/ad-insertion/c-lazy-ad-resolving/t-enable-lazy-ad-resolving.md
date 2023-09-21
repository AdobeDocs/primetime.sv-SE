---
description: Du kan aktivera eller inaktivera funktionen Lazy Ad Resolving med den befintliga Lazy Ad Loading-mekanismen (Lazy Ad Resolving är inaktiverat som standard).
keywords: Lazy;Annonsupplösning;Annonsinläsning;delayLoading
title: Aktivera lat och löst
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# Aktivera lat och löst {#enable-lazy-ad-resolving}

Du kan aktivera eller inaktivera funktionen Lazy Ad Resolving med den befintliga Lazy Ad Loading-mekanismen (Lazy Ad Resolving är inaktiverat som standard).

Du kan aktivera eller inaktivera Lazy Ad Resolving genom att ringa [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) med true eller false.

* Använda det booleska värdet *hasDelayAdLoading* och *setDelayAdLoading* metoder i AdvertisingMetadata för att styra timing för annonsupplösning och placering av annonser på tidslinjen:

   * If *hasDelayAdLoading* returnerar false, TVSDK väntar tills alla annonser är lösta och placerade innan övergången till tillståndet PREPARED görs.
   * If *hasDelayAdLoading* returnerar true, tolkar TVSDK bara de initiala annonserna och övergångarna till tillståndet PREPARED.

      * De återstående annonserna löses och placeras under uppspelningen.

   * När *hasPreroll *eller *hasLivePreroll* return false, TVSDK antar att det inte finns någon förhandsgranskning och startar uppspelningen av innehållet omedelbart. Dessa är som standard inställda på true.

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

Lyssna efter `TimelineEvent`och rita om rensningsfältet varje gång du får den här händelsen.

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
