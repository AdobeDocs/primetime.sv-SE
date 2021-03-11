---
description: Du bör frisläppa en MediaPlayer-instans och resurser när du inte längre behöver MediaResource.
title: Släpp en MediaPlayer-instans och resurser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# Släpp en MediaPlayer-instans och resurser{#release-a-mediaplayer-instance-and-resources}

Du bör frisläppa en MediaPlayer-instans och resurser när du inte längre behöver MediaResource.

När du frisläpper ett `MediaPlayer`-objekt frigörs de underliggande maskinvaruresurserna som är kopplade till det här `MediaPlayer`-objektet.

Här följer några skäl till att släppa en `MediaPlayer`:

* Om du har onödiga resurser kan det påverka prestandan.
* Om flera instanser av samma videokodek inte stöds på en enhet kan uppspelningsfel uppstå för andra program.

1. Släpp `MediaPlayer`.

   ```
   function release():void;
   ```

När `MediaPlayer`-instansen har släppts kan du inte längre använda den. Om någon metod i `MediaPlayer`-gränssnittet anropas efter att det har släppts genereras ett `IllegalStateException`.