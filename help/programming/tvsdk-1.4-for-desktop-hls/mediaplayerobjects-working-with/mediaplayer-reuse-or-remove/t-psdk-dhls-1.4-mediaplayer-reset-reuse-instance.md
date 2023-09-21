---
description: När du återställer en MediaPlayer-instans återgår den till det oinitierade IDLE-läget som definierats i MediaPlayerStatus.
title: Återställa eller återanvända en MediaPlayer-instans
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Återställa eller återanvända en MediaPlayer-instans{#reset-or-reuse-a-mediaplayer-instance}

Du kan återställa, återanvända eller frigöra en MediaPlayer-instans som du inte längre behöver.

När du återställer en MediaPlayer-instans återgår den till det oinitierade IDLE-läget som definierats i MediaPlayerStatus.

Den här åtgärden är användbar i följande fall:

* Du vill återanvända en `MediaPlayer` -instans men måste läsa in en ny `MediaResource` (videoinnehåll) och ersätta föregående instans.

  Med återställning kan du återanvända `MediaPlayer` utan att frigöra resurser, skapa om `MediaPlayer`och omfördela resurser. The `replaceCurrentItem` och `replaceCurrentResource` metoder utför automatiskt dessa steg åt dig utan att du behöver anropa återställningsmetoden.

* När `MediaPlayer` har en FELstatus och måste rensas.

  >[!IMPORTANT]
  >
  >Det här är det enda sättet att återställa efter FELstatus.

1. Utlysning `reset` för att returnera `MediaPlayer` instansen till dess oinitierade tillstånd:

   ```
   function reset():void; 
   ```

1. Använd `MediaPlayer.replaceCurrentItem` eller `MediaPlayer.replaceCurrentResource` för att läsa in en annan `MediaResource`.

   >[!TIP]
   >
   >Om du vill ta bort ett fel läser du in samma `MediaResource`.

1. När du får `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` med `PREPARED` status, starta uppspelningen.
