---
description: TVSDK skickar QoS-händelser (Quality of Service) för att meddela programmet om händelser som kan påverka beräkningen av QoS-statistik, som buffring eller sökning.
title: QoS-händelser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# QoS-händelser{#qos-events}

TVSDK skickar QoS-händelser (Quality of Service) för att meddela programmet om händelser som kan påverka beräkningen av QoS-statistik, som buffring eller sökning.

Om du vill få information om alla QoS-relaterade händelser registrerar du en implementering av `MediaPlayer.QOSEventListener` med följande återanrop:

| Händelse | Betydelse |
|---|---|
| [onBufferComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferComplete()) | Buffringen är klar. |
| [onBufferStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferStart()) | Buffring har startat. |
| [onLoadInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onLoadInfo(com.adobe.mediacore.qos.LoadInfo))(loadInfo) | Ett fragment har hämtats. |
| [onOperationFailed](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html)(MediaPlayerNotification. [](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) Varningsvarning) | Ett återställningsbart fel har inträffat. |
| [onSeekComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekComplete(long))(long adjustTime) | Sökningen är klar. |
| [onSeekStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekStart()) | Sökningen startar. |