---
description: När du återställer en MediaPlayer-instans återgår den till det oinitierade IDLE-läget som definierats i MediaPlayerStatus.
seo-description: När du återställer en MediaPlayer-instans återgår den till det oinitierade IDLE-läget som definierats i MediaPlayerStatus.
seo-title: Återställa eller återanvända en MediaPlayer-instans
title: Återställa eller återanvända en MediaPlayer-instans
uuid: b376096b-0aed-4ac2-96e5-e30a4eaf742e
translation-type: tm+mt
source-git-commit: c547002eb8946f8ccc5a79d0836f3f814e823b97
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Återställ eller återanvänd en MediaPlayer-instans{#reset-or-reuse-a-mediaplayer-instance}

Du kan återställa, återanvända eller frigöra en MediaPlayer-instans som du inte längre behöver.

När du återställer en MediaPlayer-instans återgår den till det oinitierade IDLE-läget som definierats i MediaPlayerStatus.

Den här åtgärden är användbar i följande fall:

* Du vill återanvända en `MediaPlayer`-instans men måste läsa in en ny `MediaResource` (videoinnehåll) och ersätta den tidigare instansen.

   Om du återställer kan du återanvända `MediaPlayer`-instansen utan att behöva frigöra resurser, återskapa `MediaPlayer` och omallokera resurser. Metoderna `replaceCurrentItem` och `replaceCurrentResource` utför automatiskt de här stegen åt dig, utan att du behöver anropa återställningsmetoden.

* När `MediaPlayer` har status FEL och måste rensas.

   >[!IMPORTANT]
   >
   >Det här är det enda sättet att återställa efter FELstatus.

1. Anropa `reset` för att returnera `MediaPlayer`-instansen till dess oinitierade tillstånd:

   ```
   function reset():void; 
   ```

1. Använd `MediaPlayer.replaceCurrentItem` eller `MediaPlayer.replaceCurrentResource` för att läsa in en annan `MediaResource`.

   >[!TIP]
   >
   >Läs in samma `MediaResource` om du vill ta bort ett fel.

1. När du får `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` med statusen `PREPARED` startar du uppspelningen.
