---
description: Du kan återställa, återanvända eller frigöra en MediaPlayer-instans som du inte längre behöver.
title: Återanvända eller ta bort en MediaPlayer-instans
exl-id: 1ee25dd0-95e6-472d-b80c-ef9d8461302d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Återanvända eller ta bort en MediaPlayer-instans {#reuse-or-remove-a-mediaplayer-instance}

Du kan återställa, återanvända eller frigöra en MediaPlayer-instans som du inte längre behöver.

## Återställa eller återanvända en MediaPlayer-instans {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

När du återställer en `MediaPlayer` -instansen returneras till sin oinitierade IDLE-status enligt definitionen i `MediaPlayerStatus`

* Du vill återanvända en `MediaPlayer` -instans men måste läsa in en ny `MediaResource` (videoinnehåll) och ersätta föregående instans.

   Om du återställer kan du återanvända `MediaPlayer` utan att frigöra resurser, skapa om `MediaPlayer`och omfördela resurser.

* När `MediaPlayer` har statusen FEL och måste rensas.

   >[!IMPORTANT]
   >
   >Det här är det enda sättet att återställa efter FELstatus.

   1. Utlysning `reset` för att returnera `MediaPlayer` till oinitierad status:

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. Använd `MediaPlayer.replaceCurrentResource()` för att läsa in en annan `MediaResource`.

      >[!NOTE]
      >
      >Läs in samma `MediaResource`.

   1. När du får `STATUS_CHANGED` händelseåteranrop med `PREPARED` status, starta uppspelningen.

## Släpp en MediaPlayer-instans och resurser {#section_13A0914AFF784943ABC343F7EB249C4E}

Du bör släppa en `MediaPlayer` -instans och -resurser när du inte längre behöver `MediaResource`.

När du släpper en `MediaPlayer` objekt, de underliggande maskinvaruresurserna som är kopplade till detta `MediaPlayer` -objektet har frigjorts.

Här är några skäl att släppa en `MediaPlayer`:

* Om du har onödiga resurser kan det påverka prestandan.
* Leder en onödig `MediaPlayer` objekt som instansierats kan leda till kontinuerlig batteriförbrukning för mobila enheter.
* Om flera instanser av samma videokodek inte stöds på en enhet kan uppspelningsfel uppstå för andra program.

* Släpp `MediaPlayer`.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >Efter `MediaPlayer` -instansen släpps, du kan inte längre använda den. Om någon metod i `MediaPlayer` -gränssnittet anropas när det har släppts, `MediaPlayerException` kastas.
