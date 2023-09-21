---
description: Du kan välja att använda standardbeteenden för annonser.
title: Använd standardbeteendet för uppspelning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
