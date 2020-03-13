---
description: Med metoderna i klassen MediaPlayerItem kan du hämta information om innehållsströmmen som representeras av en inläst MediaResource.
seo-description: Med metoderna i klassen MediaPlayerItem kan du hämta information om innehållsströmmen som representeras av en inläst MediaResource.
seo-title: MediaPlayerItem-metoder för åtkomst av MediaResource-information
title: MediaPlayerItem-metoder för åtkomst av MediaResource-information
uuid: 46845583-0a76-4411-a8bc-0a16ebfe8e6e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# MediaPlayerItem-metoder för åtkomst av MediaResource-information {#mediaplayeritem-methods-for-accessing-mediaresource-information}

Med metoderna i klassen MediaPlayerItem kan du hämta information om innehållsströmmen som representeras av en inläst MediaResource.

| Metod | Beskrivning |
|--- |--- |
| **Annonstaggar** |  |
| List`<String>` getAdTags() | Innehåller en lista med annonstaggar som används för annonsplaceringsprocessen. |
| **Liveström** |  |
| boolesk isLive(); | True om strömmen är live; false om det är VOD. |
| **DRM-skyddad** |  |
| boolesk isProtected(); | True om strömmen är DRM-skyddad. |
| List`<DRMMetadataInfo>` getDRMMetadataInfos(); | Visar alla DRM-metadataobjekt som identifieras i manifestet. |
| **Undertexter** |  |
| boolesk hasClosedCaptions(); | True om det finns spår för undertextning. |
| List`<ClosedCaptionsTrack>` getClosedCationsTracks(); | Innehåller en lista med tillgängliga spår för undertextning. |
| ClosedCaptionsTrack get SelectedClosedCaptionsTrack(); | Hämtar det aktuella textningsspåret som valts med SelectClosedCaptionsTrack . |
| selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) | Anger att ett undertextningsspår ska vara det aktuella undertextningsspåret. |
| **Alternativa ljudspår** |  |
| booleskt hasAlternateAudio(); | True om strömmen har alternativa ljudspår. Obs!  Huvudljudspåret (standardljudspåret) är också en del av den alternativa ljudspårslistan.  TVSDK för Android betraktar huvudljudspåret som ett av objekten i den alternativa ljudspårslistan. Därför är det enda fallet när MediaPlayerItem.hasAlternateAudio returnerar false när strömmen inte har något ljud alls. Om innehållet bara har ett ljudspår returnerar metoden true och `MediaPlayerItem.getAudioTracks` returnerar en lista med ett enda element (standardljudspåret). |
| Lista`<AudioTrack>` getAudioTracks(); | Innehåller en lista med tillgängliga alternativa ljudspår. |
| AudioTrack getSelectedAudioTrack(); | Hämtar ljudspåret som valts med selectAudioTrack . |
| selectAudioTrack ( AudioTrack audioTrack ) | Väljer att ett ljudspår ska vara aktuellt ljudspår. |
| **Tidsbestämda metadata** |  |
| boolean hasTimedMetadata(); | True if the stream has associated timed metadata. |
| List`<TimedMetadata>` getTimedMetadata(); | Innehåller en lista med tidsbestämda metadataobjekt som är associerade med strömmen. |
| **Flera profiler (bithastighet)** |
| boolean isDynamic(); | True if the stream is a multiple bit rate (MBR) stream. |
| List`<Profile>` getProfiles(); | Visar en lista med associerade bithastighetsprofiler. För varje profil kan du hämta dess bithastighet och profilens höjd och bredd. |
| Profil getSelectedProfile() | Hämtar den markerade profilen. |
| **Trick play** |  |
| booleskt isTrickPlaySupported(); | True if the player supports fast forward, rewind, and resume. |
| Lista`< Float>` getAvailablePlaybackRates() | Innehåller en lista med tillgängliga uppspelningsfrekvenser i samband med trippelfunktionen. |
| Float getSelectedPlaybackRate() | Hämtar den valda uppspelningshastigheten. |
| MediaPlayerItemConfig getConfig() | Returnerar den MediaPlayerItemConfig-instans som är associerad med det här objektet. |
| **Medieresurs** |  |
| MediaResource getResource(); | Returnerar den medieresurs som är associerad med det här objektet. |
| int getResourceId() | Returnerar medieidentifieraren som är associerad med det här objektet. Detta ID anges när objektet läses in med MediaPlayerItemLoader.load. |