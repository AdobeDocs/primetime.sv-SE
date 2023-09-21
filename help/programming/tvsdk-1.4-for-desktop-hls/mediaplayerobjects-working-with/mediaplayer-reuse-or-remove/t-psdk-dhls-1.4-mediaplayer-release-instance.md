---
description: Du bör frisläppa en MediaPlayer-instans och resurser när du inte längre behöver MediaResource.
title: Släpp en MediaPlayer-instans och resurser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Släpp en MediaPlayer-instans och resurser{#release-a-mediaplayer-instance-and-resources}

Du bör frisläppa en MediaPlayer-instans och resurser när du inte längre behöver MediaResource.

När du släpper en `MediaPlayer` objekt, de underliggande maskinvaruresurserna som är kopplade till detta `MediaPlayer` -objektet är deallokerat.

Här är några skäl att släppa en `MediaPlayer`:

* Otillräckliga resurser kan påverka prestandan.
* Om flera instanser av samma videokodek inte stöds på en enhet kan uppspelningsfel uppstå för andra program.

1. Släpp `MediaPlayer`.

   ```
   function release():void;
   ```

Efter `MediaPlayer` -instansen släpps, du kan inte längre använda den. Om någon metod i `MediaPlayer` -gränssnittet anropas när det har släppts, och `IllegalStateException` kastas.
