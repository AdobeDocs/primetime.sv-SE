---
description: När innehåll spelas upp kan webbläsarens TVSDK visa annonser och skicka information om annonser när MediaResource-objektet skapas.
seo-description: När innehåll spelas upp kan webbläsarens TVSDK visa annonser och skicka information om annonser när MediaResource-objektet skapas.
seo-title: Annonser
title: Annonser
uuid: 9a5e8c83-18ce-41e8-9cb1-fdc9da903faf
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Översikt {#ads-overview}

När innehåll spelas upp kan webbläsarens TVSDK visa annonser och skicka information om annonser när MediaResource-objektet skapas.

Du kan också anropa `prepareToPlay` funktionen efter att du har fått `AdobePSDK.MediaPlayerStatus.INITIALIZED`.

```js
function onStatusChange (event) { 
   switch (event.status) { 
     case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
        player.prepareToPlay(AdobePSDK.MediaPlayer.LIVE_POINT); 
        break; 
     case AdobePSDK.MediaPlayerStatus.PREPARED: 
        player.play(); 
        break; 
   } 
} 
 
var auditudeSettings     = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.domain  = "sample_auditude_domain"; 
auditudeSettings.mediaId = "sample_media_id"; 
auditudeSettings.zoneId  = "sample_zone_id"; 
 
// event handler 
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange); 
 
var mediaResource = new AdobePSDK.MediaResource(resourceUrl, resourceType, auditudeSettings, false);
```

Browser TVSDK innehåller även följande annonsspecifika händelser som du kan använda i händelsehanterarna för att förhindra att innehåll vidarebefordras snabbt när annonser spelas upp:

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`
* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

Om du vill se hur det fungerar i UI Framework anger du annonsinställningar i konfigurationen enligt följande:

```js
// Using UI Framework 
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
        mediaResource: { 
 
            resourceUrl:'Specify Resource Url', 
 
            auditudeSettings: { 
                validMimeTypes: ["application/x-mpeURL"], 
                domain: "Sample_auditude_domain", 
                mediaId:"sample_media_id", 
                zoneID:"sample_zone_id", 
                creativeRepackagingEnabled:true 
            } 
        } 
    } 
}; 
```

Mer information om obligatoriska metadata `AuditudeSettings`finns i [Lägg till infogningsmetadata](../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md).
