---
description: Du kan välja att använda standardbeteenden för annonser.
title: Använd standardbeteendet för uppspelning
exl-id: 8d25e076-4335-49c8-b6b8-f2694b1b9074
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---

# Använd standardbeteendet för uppspelning{#use-the-default-playback-behavior}

Du kan välja att använda standardbeteenden för annonser.

Så här använder du standardbeteenden:

* Om du implementerar en egen `ContentFactory` klass, returnera en ny instans av `DefaultAdPolicySelector` i er implementering av `doRetrieveAdPolicySelector`.

   ```
   public class CustomContentFactory extends ContentFactory { 
   
       //... 
       // your custom code for advertising classes 
       //... 
   
       /** 
        * @inheritDoc 
        */ 
       override protected function  
         doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
           return new DefaultAdPolicySelector(item); 
       } 
   }
   ```

* Om du inte har någon anpassad implementering för `ContentFactory` klass, TVSDK använder `DefaultAdPolicySelector`.
