---
description: TVSDK skickar annonsuppspelningshändelser som svar på annonsrelaterade åtgärder som när en annons börjar spelas upp.
seo-description: TVSDK skickar annonsuppspelningshändelser som svar på annonsrelaterade åtgärder som när en annons börjar spelas upp.
seo-title: Lägg till uppspelningshändelser
title: Lägg till uppspelningshändelser
uuid: dd6991ae-3e33-4d92-92e9-26b1086a555a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# Lägg till uppspelningshändelser{#ad-playback-events}

TVSDK skickar annonsuppspelningshändelser som svar på annonsrelaterade åtgärder som när en annons börjar spelas upp.

Om du vill få meddelanden om alla annonsuppspelningsrelaterade händelser registrerar du en implementering av `MediaPlayer.AdPlaybackEventListener` inklusive följande återanrop.

>[!TIP]
>
>När annonser infogas i eller tas bort från mediet skickar TVSDK uppspelningshändelsen [onTimelineUpdated](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated()).

| Händelse | Betydelse |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | Ett reklamavbrott har spelat helt. |
| onAdBreakSkipped | En annonsbrytning hoppades över under uppspelning. |
| [onAdBreakStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | En annonsbrytning har börjat. |
| [onAdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick)) (AdBreak adBreak, Ad ad ad, AdClick adClick) | Användaren har klickat på annonsen. Ger information till ditt program om annonsen som användaren klickade på som svar på att ditt program anropade `notifyClick` på `MediaPlayerView`. |
| [onAdComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak, Ad ad ad) | En annons har spelat helt och hållet. |
| [onAdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int)) (AdBreak adBreak, Ad ad ad, int percentage) | Annonsuppspelningen har fortskridit. Skickas flera gånger medan en annons spelas upp. |
| [onAdStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad)) (AdBreak adBreak, Ad ad ad) | En annons har börjat. |