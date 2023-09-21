---
description: Full-event replay (FER) är en VOD-resurs som fungerar som en live/DVR-resurs, så programmet måste vidta åtgärder för att se till att annonserna placeras på rätt sätt.
title: Aktivera annonser i repriser vid helhändelse
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Aktivera annonser i repriser vid helhändelse {#enable-ads-in-full-event-replay}

Full-event replay (FER) är en VOD-resurs som fungerar som en live/DVR-resurs, så programmet måste vidta åtgärder för att se till att annonserna placeras på rätt sätt.

För direktsänt innehåll använder TVSDK metadata/cues i manifestet för att avgöra var annonserna ska placeras. Ibland liknar dock direktsänt eller linjärt innehåll VOD-innehåll. När live-innehåll är klart, till exempel, en `EXT-X-ENDLIST` -taggen läggs till i det aktiva manifestet. För HLS är `EXT-X-ENDLIST` -taggen betyder att strömmen är en VOD-ström. För att annonser ska kunna infogas korrekt kan TVSDK inte automatiskt skilja den här strömmen från en vanlig VOD-ström.

Programmet måste informera TVSDK om innehållet är live eller VOD genom att ange `AdSignalingMode`.

För en FER-ström bör Adobe Primetime annonsbeslutsserver inte innehålla en lista över annonsbrytningar som måste infogas på tidslinjen innan uppspelningen startar. Detta är den typiska processen för VOD-innehåll. Om du anger ett annat signeringsläge läser TVSDK i stället alla referenspunkter från FER-manifestet och går till annonsservern för varje referenspunkt för att begära en annonsbrytning. Den här processen liknar live-/DVR-innehåll.

>[!TIP]
>
>Förutom varje begäran som är associerad med en referenspunkt gör TVSDK en extra annonsbegäran för annonser före rullning.

1. Hämta det signeringsläge som ska användas från en extern källa, till exempel vCMS.
1. Skapa reklamrelaterade metadata.
1. Om standardbeteendet måste skrivas över anger du `AdSignalingMode` genom att använda `AdvertisingMetadata.setSignalingMode`.

   Giltiga värden är `DEFAULT`, `SERVER_MAP`och `MANIFEST_CUES`.

   >[!IMPORTANT]
   >
   >Du måste ange annonssignaleringsläget innan du anropar `prepareToPlay`. När TVSDK börjar matcha och placera annonser på tidslinjen ignoreras ändringar av annonseringssigneringsläget. Ange läge när du skapar `AuditudeSettings` -objekt.

1. Fortsätt till uppspelningen.

<!--<a id="example_6DECA71C3C3B4551805C09A80686552F"></a>-->

```java
MediaPlayer mediaPlayer =  
  new MediaPlayer(getActivity.().getApplicationContext()); 
 
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings.setSignalingMode(AdSignalingMode.MANIFEST_CUES); 
auditudeSettings.setDomain("your-auditude-domain"); 
auditudeSettings.setZoneId("your-auditude-zone-id"); 
auditudeSettings.setMediaId("your-media-id"); 
// set additional targeting parameters or custom parameters 
 
MediaPlayerItemConfig itemConfig =  
  new MediaPlayerItemConfig(getActivity().getApplicationContext()); 
MediaResource mediaResource =  
  new MediaResource("https://example.com/media/test_media.m3u8",  
                    MediaResource.Type.HLS, Metadata); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (status == MediaPlayerStatus.INITIALIZED) { 
            mediaPlayer.prepareToPlay(); 
        } 
        else if( event.getStatus() == MediaPlayerStatus.PREPARED ) { 
            // TVSDK is in the PREPARED state, so start the playback 
            mediaPlayer.play(); 
        } 
        else if( event.getStatus() == MediaPlayerStatus.COMPLETE ) { 
            // playback has reached the end of stream ( ads included ) 
            // if we want to rewind we can call 
            mediaPlayer.seek(mediaPlayer.getSeekableRange().getBegin()); 
        } 
    } 
}); 
 
mediaPlayer.replaceCurrentResource(mediaResource, itemConfig); 
```
