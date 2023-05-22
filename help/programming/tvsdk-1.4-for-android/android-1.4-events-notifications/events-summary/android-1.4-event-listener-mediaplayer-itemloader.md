---
description: TVSDK skickar mediespelarobjektshändelser som svar på inläsning av ett mediaobjekt.
title: Loader-händelser
exl-id: 80a503f2-ad2e-44e5-93dc-2311df77f52e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
