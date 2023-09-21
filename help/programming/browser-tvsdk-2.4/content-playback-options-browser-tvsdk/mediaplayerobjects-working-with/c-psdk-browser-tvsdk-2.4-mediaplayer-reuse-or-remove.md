---
description: Du kan återställa, återanvända eller frigöra en MediaPlayer-instans som du inte längre behöver.
title: Återanvända eller ta bort en MediaPlayer-instans
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Återanvända eller ta bort en MediaPlayer-instans{#reuse-or-remove-a-mediaplayer-instance}

Du kan återställa, återanvända eller frigöra en MediaPlayer-instans som du inte längre behöver.

## Återställa eller återanvända en MediaPlayer-instans {#section_C183E6164C184C3CBC5321FC6A2528EA}

Du kan återställa en `MediaPlayer` -instans för att returnera den till det oinitierade IDLE-läget enligt definitionen i `MediaPlayerStatus`. Du kan också ersätta det aktuella mediaobjektet eller ange ett nytt med en tidigare inläst medieresurs.

Den här åtgärden är användbar i följande fall:

* Du vill återanvända en `MediaPlayer` -instans men måste läsa in en ny `MediaResource` (videoinnehåll) och ersätta föregående instans.

  Med återställning kan du återanvända `MediaPlayer` utan att frigöra resurser, skapa om `MediaPlayer`och omfördela resurser. The `replaceCurrentItem` utförs dessa steg automatiskt.

* När `MediaPlayer` är i ett FEL-tillstånd och måste rensas.

  >[!IMPORTANT]
  >
  >Det här är det enda sättet att återställa efter FELstatus.

1. Utlysning `MediaPlayer.reset()` för att returnera `MediaPlayer` instansen till dess oinitierade tillstånd:

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. Utlysning `MediaPlayer.replaceCurrentItem()` för att läsa in en annan `MediaResource`

   >[!TIP]
   >
   >Om du vill ta bort ett fel läser du in samma `MediaResource`.

1. Ring `prepareToPlay()` -metod.

   >[!NOTE]
   >
   >När du får `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` -händelsen med läget PREPARED kan du starta uppspelningen.

## Släpp en MediaPlayer-instans och resurser {#section_2D159975C82245098E7078FE0B1578CE}

Du bör släppa en `MediaPlayer` -instans och -resurser när du inte längre behöver MediaResource.

Här är några skäl att släppa en `MediaPlayer`:

* Otillräckliga resurser kan påverka prestandan.
* Leder en onödig `MediaPlayer` kan leda till kontinuerlig batteriförbrukning för mobila enheter.
* Om flera instanser av samma videokodek inte stöds på en enhet kan uppspelningsfel uppstå för andra program.

* Släpp `MediaPlayer`.

  ```js
  void release()
  ```

  >[!NOTE]
  >
  >Efter `MediaPlayer` -instansen släpps, du kan inte längre använda den. Om någon metod i `MediaPlayer` -gränssnittet anropas när det har släppts, och `IllegalStateException` kastas.
