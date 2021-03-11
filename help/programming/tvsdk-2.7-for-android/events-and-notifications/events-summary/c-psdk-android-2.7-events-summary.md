---
description: Programmet kan övervaka aktiviteten i spelaren och spelarens föränderliga status genom att avlyssna händelser som skickas av TVSDK.
title: Sammanfattning av händelser för Primetime Player
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# Sammanfattning av händelser i Primetime-spelaren {#primetime-player-events-summary-overview}

Programmet kan övervaka aktiviteten i spelaren och spelarens föränderliga status genom att avlyssna händelser som skickas av TVSDK.

## Händelser {#events}

TVSDK meddelar dig när händelser inträffar som programmet måste svara på. Varje händelse motsvarar en avlyssnarklass, med en callback-metod som du måste implementera.

>[!TIP]
>
>Händelsekoderna är konstanterna för `MediaPlayerEvent`-uppräkningen.

## AdBreakCompletedEventListener {#section_D7A74A4EACA44E54806D040491B7D879}

* ** Betydelse ** Uppspelningen av annonsbrytningen är klar.

* ** Återanrop som ska implementeras ** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* ** Händelsekod ** `AD_BREAK_COMPLETE`

## AdBreakSkippedEventListener {#section_7AE5442442484F45B521D3309691C59C}

* ** Betydelse ** En annonsbrytning hoppades över under uppspelning.

* ** Återanrop som ska implementeras ** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* ** Händelsekod ** `AD_BREAK_SKIPPED`

## AdBreakStartedEventListener {#section_0D50327621164E3A9C8F3337AA20BDE7}

* ** Betydelse ** Uppspelningen av annonsbrytning har startat.

* ** Återanrop som ska implementeras ** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* ** Händelsekod ** `AD_BREAK_START`

## AdClickEventListener {#section_9A6FD39EEDE0460B94FD074B5C2FB9BE}

* ** Betydelse ** En annons klickades under uppspelningen.

* ** Återanrop som ska implementeras ** `onAdClicked(AdClickEvent event)`

* ** Händelsekod ** `AD_CLICK`

## AdCompletedEventListener {#section_D45EA0B1825145259EAC50A3E6B24BFC}

* ** Betydelse ** Uppspelningen av annonsen är klar.

* ** Återanrop som ska implementeras ** `onAdCompleted(AdPlaybackEvent event)`

* ** Händelsekod ** `AD_COMPLETE`

## AdProgressEventListener {#section_C26ACC4B941942B0A24DB06585EF52AB}

* ** Betydelse ** Rapporterar förlopp under uppspelning.

* ** Återanrop som ska implementeras ** `onAdProgress(AdPlaybackEvent event)`

* ** Händelsekod ** `AD_PROGRESS`

## AdResolutionCompleteEventListener {#section_E9D545408CBA448EA2A8606DA629FB0B}

* ** Betydelsen ** Primetimes annonsbeslutsupplösning är klar. Den här händelsen gäller endast VOD-innehåll.

* ** Återanrop som ska implementeras ** `onAdResolutionComplete()`

* ** Händelsekod ** `AD_RESOLUTION_COMPLETE`

## AdStartedEventListener {#section_A4339C48F82640A8AF4AF09CB3B33188}

* ** Betydelse ** Uppspelningen av annonsen har startat.

* ** Återanrop som ska implementeras ** `onAdStarted(AdPlaybackEvent event)`

* ** Händelsekod ** `AD_START`

## AudioUpdatedEventListener {#section_06E1A9F683E1411081CFC6BD30C3B669}

* ** Betydelse ** Ett nytt ljudspår har identifierats.

* ** Återanrop som ska implementeras ** `onAudioUpdated(MediaPlayerItemEvent event)`

* ** Händelsekod ** `AUDIO_TRACK_UPDATED`

## BufferingBeginEventListener {#section_F8378841149A4801867ADDC7C0A98C57}

* ** Betydelse ** Spelaren har börjat buffra.

* ** Återanrop som ska implementeras ** `onBufferingBegin(BufferEvent event)`

* ** Händelsekod ** `BUFFERING_BEGIN`

## BufferingEndEventListener {#section_9107E0ED59474F11A04E243C6B117E21}

* ** Betydelse ** Spelaren har slutat buffra.

* ** Återanrop som ska implementeras ** `onBufferingEnd(BufferEvent event)`

* ** Händelsekod ** `BUFFERING_END`

## BufferPreparedEventListener {#section_F6BFDF525D8B41B7B6E0EFCCE3065811}

* ** Betydelse ** Bufferten förbereds.

* ** Återanrop som ska implementeras ** `onBufferPrepared()`

* ** Händelsekod ** `BUFFER_PREPARED`

## CaptionsUpdatedEventListener {#section_048BB128ADB747519F02DEDDD1C88B86}

* ** Betydelse ** Ett nytt bildtextspår har identifierats.

* ** Återanrop som ska implementeras ** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* ** Händelsekod ** `CAPTIONS_UPDATED`

## DRMMetadataInfoEventListener {#section_CB55064D305A40D5BBAD09A53D63DB95}

* ** Betydelse ** En ny DRM-metadata har identifierats i medieströmmen.

* ** Återanrop som ska implementeras ** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* ** Händelsekod ** `DRM_METADATA`

## ItemCreatedEventListener {#section_32A3178664C841008370E8447C978AB2}

* ** Betydelse ** Ett nytt mediespelarobjekt har skapats.

* ** Återanrop som ska implementeras ** `onItemCreated(MediaPlayerItemEvent event)`

* ** Händelsekod ** `ITEM_CREATED`

## ItemLoadCompleteEventListener {#section_E29A3D7D2666461599909BD8E8BA46A7}

* ** Betydelse ** Ny inläsningsinformation har skapats för det aktuella objektet.

* ** Återanrop som ska implementeras ** `onLoadComplete(MediaPlayerItemEvent event)`

* ** Händelsekod ** `ITEM_UPDATED`

## LoadInformationEventListener {#section_A986AD83F68446B99EAC888F98B39148}

* ** Betydelse ** Ett nytt segment har lästs in.

* ** Återanrop som ska implementeras ** `onLoadInformation(LoadInformationEvent event)`

* ** Händelsekod ** `LOAD_INFORMATION_AVAILABLE`

## MainManifestUpdatedEventListener {#section_73709D121CED48C1B38550135DA55548}

* ** Betydelse ** Huvudmanifestet eller spellistan har uppdaterats.

* ** Återanrop som ska implementeras ** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* ** Händelsekod ** `MANIFEST_UPDATED`

## NotificationEventListener {#section_E8F27B979D374B5D8EA184E23BC17E43}

* ** Betydelse ** Åtgärden misslyckades.

* ** Återanrop som ska implementeras ** `onNotification(NotificationEvent event)`

* ** Händelsekod ** `OPERATION_FAILED`

## PlaybackRangeUpdatedEventListener {#section_9072862D7EB842AEA3094DAF911CDF7F}

* ** Betydelse ** Uppspelningsintervallet har uppdaterats.

* ** Återanrop som ska implementeras ** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* ** Händelsekod ** `PLAYBACK_RANGE_UPDATED`

## PlaybackRatePlayingEventListener {#section_548A489ABED44F89BDF29DB9EDD348C5}

* ** Betydelse ** En ny uppspelningshastighet visas på skärmen.

* ** Återanrop som ska implementeras ** `onRatePlaying(PlaybackRateEvent event)`

* ** Händelsekod ** `RATE_PLAYING`

## PlaybackRateSelectedEventListener {#section_B303BAAFA6D14C1599AD3D7D79D722DD}

* ** Betydelse ** Attributet rate för MediaPlayer har angetts.

* ** Återanrop som ska implementeras ** `onRateSelected(PlaybackRateEvent event)`

* ** Händelsekod ** `RATE_SELECTED`

## PlayStartEventListener {#section_1D54CAE387B243679348A26E65B6A3FD}

* ** Betydelse ** Uppspelningen har startat.

* ** Återanrop som ska implementeras ** `onPlayStart()`

* ** Händelsekod ** `PLAY_START`

## ProfileChangeEventListener {#section_EEDF08916D1D40509E64EC180F143C9A}

* ** Betydelse ** MediaPlayers aktuella profil har ändrats.

* ** Återanrop som ska implementeras ** `onProfileChanged(ProfileEvent event)`

* ** Händelsekod ** `PROFILE_CHANGED`

## ReservationReachedEventListener {#section_31677E931F154E7E86D725B2B046065C}

* ** Betydelse ** Uppspelningen har nått en tidsgräns.

* ** Återanrop som ska implementeras ** `onReservationReached(ReservationEvent event)`

* ** Händelsekod ** `RESERVATION_REACHED`

## SeekBeginEventListener {#section_749E02ED2B1647438F50224C85260A1D}

* ** Betydelse ** Sökåtgärden har startats.

* ** Återanrop som ska implementeras ** `onSeekBegin(SeekEvent event)`

* ** Händelsekod ** `SEEK_BEGIN`

## SeekEndEventListener {#section_4F70BAD695AF4717B2254D9DBA1071E4}

* ** Betydelse ** Sökningen är klar.

* ** Återanrop som ska implementeras ** `onSeekEnd(SeekEvent event)`

* ** Händelsekod ** `SEEK_END`

## SeekPositionAdjustedEventListener {#section_01F89B73DBB84BEBBA60D820BF5FAC9A}

* ** Betydelse ** Sökpositionen har justerats på grund av interna uppspelningsregler eller externa affärsregler.

* ** Återanrop som ska implementeras ** `onPositionAdjusted(SeekEvent event)`

* ** Händelsekod ** `SEEK_POSITION_ADJUSTED`

## SizeAvailableEventListener {#section_90DF6565E59B44B19338A7B89D53BBBF}

* ** Betydelse ** Mediets storlek är tillgänglig.

* ** Återanrop som ska implementeras ** `onSizeAvailable(SizeAvailableEvent event)`

* ** Händelsekod ** `SIZE_AVAILABLE`

## StatusChangeEventListener {#section_310D2327089D46358F9CE03EA76F3287}

* ** Betydelse ** MediaPlayer-läget har ändrats.

* ** Återanrop som ska implementeras ** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* ** Händelsekod ** `STATUS_CHANGED`

## TimeChangeEventListener {#section_ED3855BD90124D97836B2D0957AD9E0C}

* ** Betydelse ** Spelhuvudet har ändrats.

* ** Återanrop som ska implementeras ** `onTimeChanged(TimeChangeEvent event)`

* ** Händelsekod ** `TIME_CHANGED`

## TimedEventListener {#section_5E62C2C81C3B4F93B46E7518578456EA}

* ** Betydelse ** Åtgärden har slutförts med den tid som har tagits för åtgärden.

* ** Återanrop som ska implementeras ** `onTimedEvent(TimedEventEvent event)`

* ** Händelsekod ** `TIMED_EVENT`

## TidslinjeMetadataAddedInBackgroundEventListener {#section_7B923C7116154CCFBAE1FCA92C928EB2}

* ** Betydelse ** En ny tidsbestämd metadata har lagts till i ett objekt i bakgrunden.

* ** Återanrop som ska implementeras ** `onTimedMetadata(TimedMetadataEvent event)`

* ** Händelsekod ** `TIMED_METADATA_ADDED_IN_BACKGROUND`

## TimedMetadataEventListener {#section_9741EA321ACF403FB8E9AB311BAACDD7}

* ** Betydelse ** En ny tidsbestämd metadata upptäcktes i medieströmmen.

* ** Återanrop som ska implementeras ** `onTimedMetadata(TimedMetadataEvent event)`

* ** Händelsekod ** `TIMED_METADATA_AVAILABLE`

## TimelineUpdatedEventListener {#section_D0755BD2AF3347C7861395706E31B861}

* ** Betydelse ** Tidslinjen har ändrats. Annonser kan ha lagts till eller tagits bort från tidslinjen.

* ** Återanrop som ska implementeras ** `onTimelineUpdated(TimelineEvent event)`

* ** Händelsekod ** `TIMELINE_UPDATED`