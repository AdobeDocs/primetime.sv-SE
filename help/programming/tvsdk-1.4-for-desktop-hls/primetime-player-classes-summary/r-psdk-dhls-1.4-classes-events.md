---
description: Dessa klasser beskriver händelser som TVSDK skickar till din mediespelare som svar på olika aktiviteter.
seo-description: Dessa klasser beskriver händelser som TVSDK skickar till din mediespelare som svar på olika aktiviteter.
seo-title: Händelseklasser
title: Händelseklasser
uuid: 5e63d43c-6112-4958-b8cd-ccf123affd08
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Händelseklasser {#events-classes}

Dessa klasser beskriver händelser som TVSDK skickar till din mediespelare som svar på olika aktiviteter.

Paket: [com.adobe.mediacore.events](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/package-detail.html)

| Namn | Betydelse |
|---|---|
| [AdBreakPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html) | Klass. En annonsbrytning påbörjades eller slutfördes. |
| [AdClickEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html) | Klass. Användaren klickade på en annons. |
| [AdPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html) | Klass. Spelaren spelade en annons. |
| [BufferEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html) | Klass. Spelaren började eller slutade buffra. |
| [CustomAdEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/CustomAdEvent.html) | Klass. Spelaren visar anpassad annonsstatus och kan ignorera annonser som innehåller fel eller tar för lång tid att läsa in. |
| [DRMMetadataInfoEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html) | Klass. Nya DRM-metadata är associerade med det aktuella objektet. |
| [LoadInformationEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/LoadInformationEvent.html) | Klass. Det finns hämtningsinformation för den aktuella medieströmmen som spelas upp. |
| [MediaPlayerItemEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html) | Klass. Ett mediespelarobjekt har skapats. |
| [MediaPlayerItemLoaderEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemLoaderEvent.html) | Klass. En inläsningsåtgärd har slutförts. Skickas av `MediaPlayerItemLoader` för att meddela sina kunder. |
| [MediaPlayerStatusChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html) | Klass. Mediespelarens status har ändrats. |
| [MediaPlayerViewEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerViewEvent.html) | Klass. Klickade `MediaPlayerView` på bilden. |
| [PlaybackRateEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html) | Klass. Mediespelarens uppspelningshastighet ändras. |
| [ProfileEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html) | Klass. Mediespelarens adaptiva bytesalgoritm för bithastighet har växlat till en annan profil på grund av nätverks- eller datorförhållanden. |
| [SeekEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html) | Klass. Spelaren började söka eller sökningen slutfördes. |
| [SizeAvailableEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SizeAvailableEvent.html) | Klass. Videostorleken är tillgänglig. |
| [TimeChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html) | Klass. Mediespelarens status har ändrats. |
| [TimedMetadataEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html) | Klass. En tidsbestämd metadata bearbetas av affärsmöjlighetsidentifieraren. |
| [TimelineEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html) | Klass. Mediespelarens tidslinje har ändrats. |