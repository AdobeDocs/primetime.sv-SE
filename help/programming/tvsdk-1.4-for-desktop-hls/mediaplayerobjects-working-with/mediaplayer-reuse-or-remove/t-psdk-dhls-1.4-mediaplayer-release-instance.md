---
description: Du bör frisläppa en MediaPlayer-instans och resurser när du inte längre behöver MediaResource.
seo-description: Du bör frisläppa en MediaPlayer-instans och resurser när du inte längre behöver MediaResource.
seo-title: Släpp en MediaPlayer-instans och resurser
title: Släpp en MediaPlayer-instans och resurser
uuid: e7b2112e-8add-4789-9345-5f829d39d639
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '141'
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