---
description: TVSDK skickar mediespelarobjektshändelser som svar på inläsning av ett mediaobjekt.
title: Loader-händelser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Loader-händelser{#loader-events}

TVSDK skickar mediespelarobjektshändelser som svar på inläsning av ett mediaobjekt.

Dessa händelser utgör ett alternativt arbetsflöde. Du behöver inte implementera det här gränssnittet när du skapar en `MediaPlayer`. Använd detta när du vill ha en `MediaPlayerItemLoader`.

Om du vill få meddelanden om händelser som rör inläsning av en mediespelarresurs registrerar du avlyssnare för följande händelser med `MediaPlayerItemLoader` -objekt.

| Händelse | Betydelse |
|---|---|
| MediaPlayerItemLoader.[slutförd](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | Inläsningen av medieresursen har slutförts. |
| MediaPlayerItemLoader.[misslyckades](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | Ett problem uppstod vid inläsning av medieresurser. |
