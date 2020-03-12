---
description: Du kan visa längden på det aktiva innehållet.
seo-description: Du kan visa längden på det aktiva innehållet.
seo-title: Visa videons längd
title: Visa videons längd
uuid: 945f222d-80ba-4832-a06f-9bb8db6adbcb
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d

---


# Visa videons längd {#display-the-duration-of-the-video}

Du kan visa längden på det aktiva innehållet.

Implementera en video-duration-visning med följande exempelkod:

    Egenskapen &quot;PTMediaPlayer&quot;, &quot; [seekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange)&quot;, innehåller det aktuella sökbara fönsterintervallet:
    
    * För VOD är det här intervallet hela VOD-innehållsområdet, inklusive annonser.
    * För live/linear representerar detta intervall fönstret som kan sökas.
    
    Mer information om API:t finns i [TVSDK 3.4 for iOS API Reference](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v3/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
