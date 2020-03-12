---
description: Du kan återställa, återanvända eller frigöra en MediaPlayer-instans som du inte längre behöver.
seo-description: Du kan återställa, återanvända eller frigöra en MediaPlayer-instans som du inte längre behöver.
seo-title: Återanvända eller ta bort en MediaPlayer-instans
title: Återanvända eller ta bort en MediaPlayer-instans
uuid: 0b9a06b0-ece7-4e18-9221-a4528bcbc141
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Återanvända eller ta bort en MediaPlayer-instans{#reuse-or-remove-a-mediaplayer-instance}

Du kan återställa, återanvända eller frigöra en MediaPlayer-instans som du inte längre behöver.

## Återställa eller återanvända en MediaPlayer-instans {#section_C183E6164C184C3CBC5321FC6A2528EA}

Du kan återställa en `MediaPlayer` instans så att den återgår till sitt oinitierade IDLE-läge enligt definitionen i `MediaPlayerStatus`. Du kan också ersätta det aktuella mediaobjektet eller ange ett nytt med en tidigare inläst medieresurs.

Den här åtgärden är användbar i följande fall:

* Du vill återanvända en `MediaPlayer` instans men måste läsa in ett nytt `MediaResource` (videoinnehåll) och ersätta föregående instans.

   Om du återställer kan du återanvända `MediaPlayer` instansen utan att behöva frigöra resurser, återskapa `MediaPlayer`och omfördela resurser. Metoden utför automatiskt dessa steg åt dig `replaceCurrentItem` .

* När `MediaPlayer` är i ett FEL-läge och måste rensas.

   >[!IMPORTANT]
   >
   >Det här är det enda sättet att återställa efter FELstatus.

1. Anropa `MediaPlayer.reset()` för att returnera `MediaPlayer` instansen till dess oinitierade tillstånd:

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. Ring `MediaPlayer.replaceCurrentItem()` för att ladda en till `MediaResource`

   >[!TIP]
   >
   >Om du vill ta bort ett fel läser du in samma `MediaResource`.

1. Anropa `prepareToPlay()` metoden.

   >[!NOTE]
   >
   >När du tar emot en `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` händelse med tillståndet PREPARED kan du starta uppspelningen.

## Släpp en MediaPlayer-instans och resurser {#section_2D159975C82245098E7078FE0B1578CE}

Du bör frisläppa en `MediaPlayer` instans och resurser när du inte längre behöver MediaResource.

Här är några skäl att släppa en `MediaPlayer`:

* Om du har onödiga resurser kan det påverka prestandan.
* Om du lämnar ett onödigt `MediaPlayer` objekt kan det leda till kontinuerlig batteriförbrukning för mobila enheter.
* Om flera instanser av samma videokodek inte stöds på en enhet kan uppspelningsfel uppstå för andra program.

* Släpp `MediaPlayer`.

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >När `MediaPlayer` instansen har släppts kan du inte längre använda den. Om någon metod i `MediaPlayer` gränssnittet anropas efter att det har släppts `IllegalStateException` genereras ett fel.

