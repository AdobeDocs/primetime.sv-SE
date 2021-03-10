---
description: TVSDK skickar annonsuppspelningshändelser som svar på annonsrelaterade åtgärder som när en annons börjar spelas upp.
title: Lägg till uppspelningshändelser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# Lägg till uppspelningshändelser {#ad-playback-events}

TVSDK skickar annonsuppspelningshändelser som svar på annonsrelaterade åtgärder som när en annons börjar spelas upp.

Om du vill få meddelanden om alla annonsuppspelningsrelaterade händelser registrerar du avlyssnare med `MediaPlayer`-objektet för följande händelser.

>[!TIP]
>
>När annonser infogas i eller tas bort från mediet skickar TVSDK uppspelningshändelsen TimelineEvent.[TIMELINE_UPDATED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED).

| Händelse | Betydelse |
|---|---|
| AdBreakPlaybackEvent.[AD_BREAK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | Ett reklamavbrott har spelat helt. |
| AdBreakPlaybackEvent.[AD_BREAK_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | En annonsbrytning hoppades över under uppspelning. |
| AdBreakPlaybackEvent.[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | En annonsbrytning har börjat. |
| AdClickEvent.[AD_KLICKA](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | Användaren har klickat på annonsen. Ger information till ditt program om annonsen som användaren klickade på som svar på att ditt program anropade `notifyClick` på `MediaPlayerView`. |
| AdPlaybackEvent.[AD _SLUTFÖRD](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | En annons har spelat helt och hållet. |
| AdPlaybackEvent.[AD _PROGRESS](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | Annonsuppspelningen har fortskridit. Skickas flera gånger medan en annons spelas upp. |
| AdPlaybackEvent.[AD_SEEK](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | En sökning har gjorts över annonsgränserna eller inom en annons. |
| AdPlaybackEvent.[AD _STARTAD](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | En annons har börjat. |