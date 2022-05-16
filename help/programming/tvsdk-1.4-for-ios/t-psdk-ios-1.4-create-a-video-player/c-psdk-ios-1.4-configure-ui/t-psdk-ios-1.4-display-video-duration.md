---
description: Du kan visa längden på det aktiva innehållet.
title: Visa videons längd
exl-id: 4e31d784-4d16-470b-8317-11be32a55c2f
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Visa videons längd {#display-the-duration-of-the-video}

Du kan visa längden på det aktiva innehållet.

Implementera en video-duration-visning med följande exempelkod:

The `PTMediaPlayer` egenskap, [seekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange), innehåller det aktuella sökbara fönsterintervallet:

* För VOD är detta intervall hela VOD-innehållsområdet, inklusive annonser.
* För live/linjärt representerar detta intervall det sökbara fönstret.

Mer information om API:t finns i [TVSDK 1.4 för API-referens för iOS](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
