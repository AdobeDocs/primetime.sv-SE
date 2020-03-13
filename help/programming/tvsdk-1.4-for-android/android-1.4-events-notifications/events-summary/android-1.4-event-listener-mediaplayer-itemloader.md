---
description: TVSDK skickar mediespelarobjektshändelser som svar på inläsning av ett mediaobjekt.
seo-description: TVSDK skickar mediespelarobjektshändelser som svar på inläsning av ett mediaobjekt.
seo-title: Loader-händelser
title: Loader-händelser
uuid: 1b401ff5-4313-4c64-8be9-99bdeb58ba2a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Loader-händelser{#loader-events}

TVSDK skickar mediespelarobjektshändelser som svar på inläsning av ett mediaobjekt.

Dessa händelser utgör ett alternativt arbetsflöde. Du behöver inte implementera det här gränssnittet när du skapar en MediaPlayer. Använd den här när du vill ha en `MediaPlayerItemLoader`.

Om du vill få meddelanden om händelser som rör inläsning av en mediespelarresurs registrerar du en implementering av `MediaPlayerItemLoader.LoaderListener` inklusive följande händelser.

| Händelse | Betydelse |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([mediaPlayerItem](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) playerItem) | Inläsningen av medieresursen har slutförts. |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | Ett problem uppstod vid inläsning av medieresurser. |

>[!NOTE]
>
>Se även `onLoadInfo (loadInfo)` under QoS-händelser.

