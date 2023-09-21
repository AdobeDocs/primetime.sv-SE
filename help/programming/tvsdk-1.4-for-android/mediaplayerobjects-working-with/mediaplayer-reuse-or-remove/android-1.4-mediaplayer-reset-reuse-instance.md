---
description: När du återställer en MediaPlayer-instans återgår den till det oinitierade IDLE-läget som definierats i MediaPlayerState.
title: Återställa eller återanvända en MediaPlayer-instans
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Återställ, återanvända eller ta bort en MediaPlayer-instans {#reset-or-reuse-a-mediaplayer-instance}

Du kan återställa, återanvända eller frigöra en MediaPlayer-instans som du inte längre behöver.

När du återställer en MediaPlayer-instans återgår den till det oinitierade IDLE-läget som definierats i MediaPlayerState.

Den här åtgärden är användbar i följande fall:

* Du vill återanvända en `MediaPlayer` -instans men måste läsa in en ny `MediaResource` (videoinnehåll) och ersätta föregående instans.

  Med återställning kan du återanvända `MediaPlayer` utan att frigöra resurser, skapa om `MediaPlayer`och omfördela resurser.

* När `MediaPlayer` är i ett FEL-tillstånd och måste rensas.

  >[!IMPORTANT]
  >
  >Det här är det enda sättet att återställa efter FELstatus.

1. Utlysning `reset` för att returnera `MediaPlayer` instansen till dess oinitierade tillstånd:

   ```java
   void reset() throws IllegalStateException; 
   ```

1. Använd `MediaPlayer.replaceCurrentResource` för att läsa in en annan `MediaResource`.

   >[!TIP]
   >
   >Om du vill ta bort ett fel läser du in samma `MediaResource`.

1. När du får `STATUS_CHANGED` händelseåteranrop med statusen PREPARED, starta uppspelningen.

## Släpp en MediaPlayer-instans och resurser{#release-a-mediaplayer-instance-and-resources}

Du bör frisläppa en MediaPlayer-instans och resurser när du inte längre behöver MediaResource.

När du släpper en `MediaPlayer` objekt, de underliggande maskinvaruresurserna som är kopplade till detta `MediaPlayer` -objektet är deallokerat.

Här är några skäl att släppa en MediaPlayer:

* Otillräckliga resurser kan påverka prestandan.
* Leder en onödig `MediaPlayer` kan leda till kontinuerlig batteriförbrukning för mobila enheter.
* Om flera instanser av samma videokodek inte stöds på en enhet kan uppspelningsfel uppstå för andra program.

1. Släpp `MediaPlayer`.

   ```java
   void release() throws IllegalStateException;
   ```

Efter `MediaPlayer` -instansen släpps, du kan inte längre använda den. Om någon metod i `MediaPlayer` -gränssnittet anropas när det har släppts, och `IllegalStateException` kastas.
