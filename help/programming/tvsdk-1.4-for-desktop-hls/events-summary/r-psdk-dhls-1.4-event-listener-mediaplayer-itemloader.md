---
description: TVSDK skickar mediespelarobjektshändelser som svar på inläsning av ett mediaobjekt.
seo-description: TVSDK skickar mediespelarobjektshändelser som svar på inläsning av ett mediaobjekt.
seo-title: Loader-händelser
title: Loader-händelser
uuid: 0ad37715-14b1-457c-892f-0db0d6220f0c
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Loader-händelser{#loader-events}

TVSDK skickar mediespelarobjektshändelser som svar på inläsning av ett mediaobjekt.

Dessa händelser utgör ett alternativt arbetsflöde. Du behöver inte implementera det här gränssnittet när du skapar en `MediaPlayer`. Använd den här när du vill ha en `MediaPlayerItemLoader`.

Om du vill få meddelanden om händelser som rör inläsning av en mediespelarresurs registrerar du avlyssnare för följande händelser med `MediaPlayerItemLoader` objektet.

| Händelse | Betydelse |
|---|---|
| MediaPlayerItemLoader.[slutförd](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | Inläsningen av medieresursen har slutförts. |
| MediaPlayerItemLoader.[misslyckades](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | Ett problem uppstod vid inläsning av medieresurser. |