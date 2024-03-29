---
description: Programmet kan övervaka aktiviteten i spelaren och spelarens föränderliga status genom att avlyssna händelser som skickas av TVSDK.
title: Sammanfattning av händelser för Primetime Player
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Sammanfattning av händelser för Primetime Player {#primetime-player-events-summary}

Programmet kan övervaka aktiviteten i spelaren och spelarens föränderliga status genom att avlyssna händelser som skickas av TVSDK.

## Händelser {#events}

TVSDK meddelar dig när händelser inträffar som programmet måste svara på. Varje händelse motsvarar en avlyssnarklass, med en callback-metod som du måste implementera.

>[!TIP]
>
>Händelsekoderna är konstanterna för `MediaPlayerEvent` enum.

`AdBreakCompletedEventListener`

* **Betydelse** Annonsbrytningen har spelats upp.

* **Återanrop som ska implementeras** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **Händelsekod** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **Betydelse** En annonsbrytning hoppades över under uppspelning.

* **Återanrop som ska implementeras** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **Händelsekod** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **Betydelse** Uppspelningen av en annonsbrytning har startat.

* **Återanrop som ska implementeras** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **Händelsekod** `AD_BREAK_START`

`AdClickedEventListener`

* **Betydelse** En annons klickades under uppspelningen.

* **Återanrop som ska implementeras** `onAdClicked(AdClickEvent event)`
* **Händelsekod** `AD_CLICK`

`AdCompletedEventListener`

* **Betydelse** Uppspelningen av annonsen är klar.

* **Återanrop som ska implementeras** `onAdCompleted(AdPlaybackEvent event)`

* **Händelsekod** `AD_COMPLETE`

`AdProgressEventListener`

* **Betydelse** Rapporterar förlopp under uppspelning.

* **Återanrop som ska implementeras** `onAdProgress(AdPlaybackEvent event)`

* **Händelsekod** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **Betydelse** Primetimes annonsbeslutsupplösning är klar. Den här händelsen gäller endast VOD-innehåll.

* **Återanrop som ska implementeras** `onAdResolutionComplete()`

* **Händelsekod** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **Betydelse** Uppspelningen av annonsen har startat.

* **Återanrop som ska implementeras** `onAdStarted(AdPlaybackEvent event)`

* **Händelsekod** `AD_START`

`AudioUpdatedEventListener`

* **Betydelse** Ett nytt ljudspår har identifierats.

* **Återanrop som ska implementeras** `onAudioUpdated(MediaPlayerItemEvent event)`

* **Händelsekod** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **Betydelse** Spelaren har börjat buffra.

* **Återanrop som ska implementeras** `onBufferingBegin(BufferEvent event)`

* **Händelsekod** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **Betydelse** Spelaren har slutat buffra.

* **Återanrop som ska implementeras** `onBufferingEnd(BufferEvent event)`

* **Händelsekod** `BUFFERING_END`

`BufferPreparedEventListener`

* **Betydelse** Bufferten förbereds.

* **Återanrop som ska implementeras** `onBufferPrepared()`

* **Händelsekod** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **Betydelse** Ett nytt bildtextspår har identifierats.

* **Återanrop som ska implementeras** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **Händelsekod** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **Betydelse** En ny DRM-metadata har identifierats i medieströmmen.

* **Återanrop som ska implementeras** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **Händelsekod** `DRM_METADATA`

`ItemCreatedEventListener`

* **Betydelse** Ett nytt mediespelarobjekt har skapats.

* **Återanrop som ska implementeras** `onItemCreated(MediaPlayerItemEvent event)`

* **Händelsekod** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **Betydelse** Ny inläsningsinformation har skapats för det aktuella objektet.

* **Återanrop som ska implementeras** `onLoadComplete(MediaPlayerItemEvent event)`

* **Händelsekod** `ITEM_UPDATED`

`LoadInformationEventListener`

* **Betydelse** Ett nytt segment har lästs in.

* **Återanrop som ska implementeras** `onLoadInformation(LoadInformationEvent event)`

* **Händelsekod** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **Betydelse** Huvudmanifestet eller spellistan har uppdaterats.

* **Återanrop som ska implementeras** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **Händelsekod** `MANIFEST_UPDATED`

`NotificationEventListener`

* **Betydelse** Åtgärden misslyckades.

* **Återanrop som ska implementeras** `onNotification(NotificationEvent event)`

* **Händelsekod** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **Betydelse** Uppspelningsintervallet har uppdaterats.

* **Återanrop som ska implementeras** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **Händelsekod** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **Betydelse** En ny uppspelningshastighet visas på skärmen.

* **Återanrop som ska implementeras** `onRatePlaying(PlaybackRateEvent event)`

* **Händelsekod** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **Betydelse** MediaPlayers rate-attribut har angetts.

* **Återanrop som ska implementeras** `onRateSelected(PlaybackRateEvent event)`

* **Händelsekod** `RATE_SELECTED`

`PlayStartEventListener`

* **Betydelse** Uppspelningen har startat.

* **Återanrop som ska implementeras** `onPlayStart()`

* **Händelsekod** `PLAY_START`

`ProfileChangeEventListener`

* **Betydelse** MediaPlayers aktuella profil har ändrats.

* **Återanrop som ska implementeras** `onProfileChanged(ProfileEvent event)`

* **Händelsekod** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **Betydelse** Uppspelningen har nått en tidslinjereservation.

* **Återanrop som ska implementeras** `onReservationReached(ReservationEvent event)`

* **Händelsekod** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **Betydelse** Sökåtgärden har startats.

* **Återanrop som ska implementeras** `onSeekBegin(SeekEvent event)`

* **Händelsekod** `SEEK_BEGIN`

`SeekEndEventListener`

* **Betydelse** Sökåtgärden har slutförts.

* **Återanrop som ska implementeras** `onSeekEnd(SeekEvent event)`

* **Händelsekod** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **Betydelse** Sökpositionen har justerats på grund av interna uppspelningsregler eller externa affärsregler.

* **Återanrop som ska implementeras** `onPositionAdjusted(SeekEvent event)`

* **Händelsekod** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **Betydelse** Mediets storlek är tillgänglig.

* **Återanrop som ska implementeras** `onSizeAvailable(SizeAvailableEvent event)`

* **Händelsekod** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **Betydelse** MediaPlayer-läget har ändrats.

* **Återanrop som ska implementeras** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **Händelsekod** `STATUS_CHANGED`

`TimeChangeEventListener`

* **Betydelse** Spelhuvudet har ändrats.

* **Återanrop som ska implementeras** `onTimeChanged(TimeChangeEvent event)`

* **Händelsekod** `TIME_CHANGED`

`TimedEventEventListener`

* **Betydelse** Åtgärden har slutförts med den tid som har tagits för åtgärden.

* **Återanrop som ska implementeras** `onTimedEvent(TimedEventEvent event)`

* **Händelsekod** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **Betydelse** En ny tidsbestämd metadata har lagts till i ett objekt i bakgrunden.

* **Återanrop som ska implementeras** `onTimedMetadata(TimedMetadataEvent event)`

* **Händelsekod** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **Betydelse** En ny tidsbestämd metadata upptäcktes i medieströmmen.

* **Återanrop som ska implementeras** `onTimedMetadata(TimedMetadataEvent event)`

* **Händelsekod** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **Betydelse** Tidslinjen har ändrats. Annonser kan ha lagts till eller tagits bort från tidslinjen.

* **Återanrop som ska implementeras** `onTimelineUpdated(TimelineEvent event)`

* **Händelsekod** `TIMELINE_UPDATED`
