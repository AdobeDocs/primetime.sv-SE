---
description: När du återställer en MediaPlayer-instans återgår den till det oinitierade IDLE-läget som definierats i MediaPlayerState.
seo-description: När du återställer en MediaPlayer-instans återgår den till det oinitierade IDLE-läget som definierats i MediaPlayerState.
seo-title: Återställa eller återanvända en MediaPlayer-instans
title: Återställa eller återanvända en MediaPlayer-instans
uuid: 72cc4511-8ab0-44e5-b93c-b36f0321bba8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Återställ, återanvända eller ta bort en MediaPlayer-instans {#reset-or-reuse-a-mediaplayer-instance}

Du kan återställa, återanvända eller frigöra en MediaPlayer-instans som du inte längre behöver.

När du återställer en MediaPlayer-instans återgår den till det oinitierade IDLE-läget som definierats i MediaPlayerState.

Den här åtgärden är användbar i följande fall:

* Du vill återanvända en `MediaPlayer`-instans men måste läsa in en ny `MediaResource` (videoinnehåll) och ersätta den tidigare instansen.

   Om du återställer kan du återanvända `MediaPlayer`-instansen utan att behöva frigöra resurser, återskapa `MediaPlayer` och omallokera resurser.

* När `MediaPlayer` är i ett FEL-tillstånd och måste rensas.

   >[!IMPORTANT]
   >
   >Det här är det enda sättet att återställa efter FELstatus.

1. Anropa `reset` för att returnera `MediaPlayer`-instansen till dess oinitierade tillstånd:

   ```java
   void reset() throws IllegalStateException; 
   ```

1. Använd `MediaPlayer.replaceCurrentResource` för att läsa in en annan `MediaResource`.

   >[!TIP]
   >
   >Läs in samma `MediaResource` om du vill ta bort ett fel.

1. Starta uppspelningen när du får `STATUS_CHANGED`-händelseåteranropet med statusen PREPARED.

## Släpp en MediaPlayer-instans och resurser{#release-a-mediaplayer-instance-and-resources}

Du bör frisläppa en MediaPlayer-instans och resurser när du inte längre behöver MediaResource.

När du frisläpper ett `MediaPlayer`-objekt frigörs de underliggande maskinvaruresurserna som är kopplade till det här `MediaPlayer`-objektet.

Här är några skäl att släppa en MediaPlayer:

* Om du har onödiga resurser kan det påverka prestandan.
* Om du lämnar ett onödigt `MediaPlayer`-objekt kan det leda till kontinuerlig batteriförbrukning för mobila enheter.
* Om flera instanser av samma videokodek inte stöds på en enhet kan uppspelningsfel uppstå för andra program.

1. Släpp `MediaPlayer`.

   ```java
   void release() throws IllegalStateException;
   ```

När `MediaPlayer`-instansen har släppts kan du inte längre använda den. Om någon metod i `MediaPlayer`-gränssnittet anropas efter att det har släppts genereras ett `IllegalStateException`.