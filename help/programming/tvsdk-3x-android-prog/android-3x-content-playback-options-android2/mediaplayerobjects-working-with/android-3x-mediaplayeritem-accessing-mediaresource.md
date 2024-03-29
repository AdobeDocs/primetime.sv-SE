---
description: Med metoderna i klassen MediaPlayerItem kan du hämta information om innehållsströmmen som representeras av en inläst MediaResource.
title: MediaPlayerItem-metoder för åtkomst av MediaResource-information
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# MediaPlayerItem-metoder för åtkomst av MediaResource-information {#mediaplayeritem-methods-for-accessing-mediaresource-information}

Med metoderna i klassen MediaPlayerItem kan du hämta information om innehållsströmmen som representeras av en inläst MediaResource.

| Metod | Beskrivning |
|--- |--- |
| **Annonstaggar** |  |
| Lista`<String>` getAdTags() | Innehåller en lista med annonstaggar som används för annonsplaceringsprocessen. |
| **Liveström** |  |
| boolesk isLive(); | True if the stream is live; false if it is VOD. |
| **DRM-skyddad** |  |
| boolesk isProtected(); | True om strömmen är DRM-skyddad. |
| Lista`<DRMMetadataInfo>` getDRMMetadataInfos(); | Visar alla DRM-metadataobjekt som identifieras i manifestet. |
| **Undertexter** |  |
| boolesk hasClosedCaptions(); | True om det finns spår för undertextning. |
| Lista`<ClosedCaptionsTrack>` getClosedCationsTracks(); | Innehåller en lista med tillgängliga spår för undertextning. |
| ClosedCaptionsTrack get SelectedClosedCaptionsTrack(); | Hämtar det aktuella textningsspåret som valts med SelectClosedCaptionsTrack . |
| selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) | Anger att ett undertextningsspår ska vara det aktuella undertextningsspåret. |
| **Alternativa ljudspår** |  |
| booleskt hasAlternateAudio(); | True om strömmen har alternativa ljudspår. Obs! Huvudljudspåret (standardljudspåret) är också en del av den alternativa ljudspårslistan.  TVSDK för Android betraktar huvudljudspåret som ett av objekten i den alternativa ljudspårslistan. Därför är det enda fallet när MediaPlayerItem.hasAlternateAudio returnerar false när strömmen inte har något ljud alls. Om innehållet bara har ett ljudspår returnerar metoden true och  `MediaPlayerItem.getAudioTracks`  returnerar en lista med ett enda element (standardljudspåret). |
| Lista`<AudioTrack>` getAudioTracks(); | Innehåller en lista med tillgängliga alternativa ljudspår. |
| AudioTrack getSelectedAudioTrack(); | Hämtar ljudspåret som valts med selectAudioTrack . |
| selectAudioTrack ( AudioTrack audioTrack ) | Väljer att ett ljudspår ska vara aktuellt ljudspår. |
| **Tidsbestämda metadata** |  |
| boolean hasTimedMetadata(); | True if the stream has associated timed metadata. |
| Lista`<TimedMetadata>` getTimedMetadata(); | Innehåller en lista med tidsbestämda metadataobjekt som är associerade med strömmen. |
| **Flera profiler (bithastigheter)** |
| boolean isDynamic(); | True if the stream is a multiple bit rate (MBR) stream. |
| Lista`<Profile>` getProfiles(); | Innehåller en lista med associerade bithastighetsprofiler. För varje profil kan du hämta dess bithastighet och profilens höjd och bredd. |
| Profil getSelectedProfile() | Hämtar den markerade profilen. |
| **Trick play** |  |
| booleskt isTrickPlaySupported(); | True if the player supports fast forward, rewind, and resume. |
| Lista`< Float>` getAvailablePlaybackRates() | Innehåller en lista med tillgängliga uppspelningsfrekvenser i samband med trippelfunktionen. |
| Float getSelectedPlaybackRate() | Hämtar den valda uppspelningshastigheten. |
| MediaPlayerItemConfig getConfig() | Returnerar den MediaPlayerItemConfig-instans som är associerad med det här objektet. |
| **Medieresurs** |  |
| MediaResource getResource(); | Returnerar den medieresurs som är associerad med det här objektet. |
| int getResourceId() | Returnerar medieidentifieraren som är associerad med det här objektet. Detta ID anges när objektet läses in med MediaPlayerItemLoader.load. |
