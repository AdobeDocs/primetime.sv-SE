---
description: TVSDK skickar mediespelarobjektshändelser som svar på inläsning av ett mediaobjekt.
title: Loader-händelser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Loader-händelser{#loader-events}

TVSDK skickar mediespelarobjektshändelser som svar på inläsning av ett mediaobjekt.

Dessa händelser utgör ett alternativt arbetsflöde. Du behöver inte implementera det här gränssnittet när du skapar en MediaPlayer. Använd detta när du vill ha en `MediaPlayerItemLoader`.

Om du vill få meddelanden om händelser som rör inläsning av en mediespelarresurs registrerar du en implementering av `MediaPlayerItemLoader.LoaderListener` inklusive följande händelser.

| Händelse | Betydelse |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([mediaPlayerItem](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) playerItem) | Inläsningen av medieresursen har slutförts. |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | Ett problem uppstod vid inläsning av medieresurser. |

>[!NOTE]
>
>Se även `onLoadInfo (loadInfo)` under QoS-händelser.
