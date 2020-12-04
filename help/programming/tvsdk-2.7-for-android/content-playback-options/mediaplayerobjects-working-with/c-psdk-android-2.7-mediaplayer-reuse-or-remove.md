---
description: Du kan återställa, återanvända eller frigöra en MediaPlayer-instans som du inte längre behöver.
seo-description: Du kan återställa, återanvända eller frigöra en MediaPlayer-instans som du inte längre behöver.
seo-title: Återanvända eller ta bort en MediaPlayer-instans
title: Återanvända eller ta bort en MediaPlayer-instans
uuid: da7b3468-3f0f-4025-927b-d47764a053af
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---


# Återanvända eller ta bort en MediaPlayer-instans {#reuse-or-remove-a-mediaplayer-instance}

Du kan återställa, återanvända eller frigöra en MediaPlayer-instans som du inte längre behöver.

## Återställ eller återanvänd en MediaPlayer-instans {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

När du återställer en `MediaPlayer`-instans återgår den till sin oinitierade IDLE-status enligt definitionen i `MediaPlayerStatus`

* Du vill återanvända en `MediaPlayer`-instans men måste läsa in en ny `MediaResource` (videoinnehåll) och ersätta den tidigare instansen.

   Om du återställer kan du återanvända `MediaPlayer`-instansen utan att behöva frigöra resurser, återskapa `MediaPlayer` och omallokera resurser.

* När `MediaPlayer` har statusen FEL och måste rensas.

   >[!IMPORTANT]
   >
   >Det här är det enda sättet att återställa efter FELstatus.

   1. Anropa `reset` för att returnera `MediaPlayer`-instansen till dess oinitierade status:

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. Använd `MediaPlayer.replaceCurrentResource()` för att läsa in en annan `MediaResource`.

      >[!NOTE]
      >
      >Läs in samma `MediaResource` om du vill ta bort ett fel.

   1. Starta uppspelningen när du tar emot `STATUS_CHANGED`-händelseåteranropet med `PREPARED`-status.

## Släpp en MediaPlayer-instans och resurser {#section_13A0914AFF784943ABC343F7EB249C4E}

Du bör frisläppa en `MediaPlayer`-instans och resurser när du inte längre behöver `MediaResource`.

När du frisläpper ett `MediaPlayer`-objekt frigörs de underliggande maskinvaruresurserna som är kopplade till det här `MediaPlayer`-objektet.

Här följer några skäl till att släppa en `MediaPlayer`:

* Om du har onödiga resurser kan det påverka prestandan.
* Om du lämnar ett onödigt `MediaPlayer`-objekt instansierat kan det leda till kontinuerlig batteriförbrukning för mobila enheter.
* Om flera instanser av samma videokodek inte stöds på en enhet kan uppspelningsfel uppstå för andra program.

* Släpp `MediaPlayer`.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >När `MediaPlayer`-instansen har släppts kan du inte längre använda den. Om någon metod i `MediaPlayer`-gränssnittet anropas efter att det har släppts genereras ett `MediaPlayerException`.