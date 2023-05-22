---
description: Du bör frisläppa en MediaPlayer-instans och resurser när du inte längre behöver MediaResource.
title: Släpp en MediaPlayer-instans och resurser
exl-id: 2a802754-5c51-4e5f-8c36-843074b487b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Släpp en MediaPlayer-instans och resurser{#release-a-mediaplayer-instance-and-resources}

Du bör frisläppa en MediaPlayer-instans och resurser när du inte längre behöver MediaResource.

När du släpper en `MediaPlayer` objekt, de underliggande maskinvaruresurserna som är kopplade till detta `MediaPlayer` -objektet har frigjorts.

Här är några skäl att släppa en `MediaPlayer`:

* Om du har onödiga resurser kan det påverka prestandan.
* Om flera instanser av samma videokodek inte stöds på en enhet kan uppspelningsfel uppstå för andra program.

1. Släpp `MediaPlayer`.

   ```
   function release():void;
   ```

Efter `MediaPlayer` -instansen släpps, du kan inte längre använda den. Om någon metod i `MediaPlayer` -gränssnittet anropas när det har släppts, och `IllegalStateException` kastas.
