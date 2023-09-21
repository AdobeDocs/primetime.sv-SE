---
description: TVSDK skickar annonsuppspelningshändelser som svar på annonsrelaterade åtgärder som när en annons börjar spelas upp.
title: Lägg till uppspelningshändelser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Lägg till uppspelningshändelser{#ad-playback-events}

TVSDK skickar annonsuppspelningshändelser som svar på annonsrelaterade åtgärder som när en annons börjar spelas upp.

Registrera en implementering av `MediaPlayer.AdPlaybackEventListener` inklusive följande återanrop.

>[!TIP]
>
>När annonser infogas i eller tas bort från media skickar TVSDK uppspelningshändelsen [onTimelineUpdated](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated()).

| Händelse | Betydelse |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | Ett reklamavbrott har spelat helt. |
| onAdBreakSkipped | En annonsbrytning hoppades över under uppspelning. |
| [onAdBreakStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | En annonsbrytning har startat. |
| [onAdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick)) (AdBreak adBreak, Ad ad, AdClick adClick) | Användaren har klickat på annonsen. Ger information till ditt program om annonsen som användaren klickade på som svar på ditt programanrop `notifyClick` på `MediaPlayerView`. |
| [onAdComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak, Ad ad) | En annons har spelat helt och hållet. |
| [onAdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int)) (AdBreak adBreak, Ad ad ad, int percentage) | Annonsuppspelningen har fortskridit. Skickas flera gånger medan en annons spelas upp. |
| [onAdStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad)) (AdBreak adBreak, Ad ad) | En annons har börjat. |
