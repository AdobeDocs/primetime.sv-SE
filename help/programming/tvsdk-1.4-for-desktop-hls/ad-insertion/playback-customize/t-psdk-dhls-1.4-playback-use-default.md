---
description: Du kan välja att använda standardbeteenden för annonser.
seo-description: Du kan välja att använda standardbeteenden för annonser.
seo-title: Använd standardbeteendet för uppspelning
title: Använd standardbeteendet för uppspelning
uuid: 7139384c-167a-4cab-816a-c02fb723a5cb
translation-type: tm+mt
source-git-commit: 1985694f99c548284aad6e6b4e070bece230bdf4
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# Använd standardbeteendet för uppspelning{#use-the-default-playback-behavior}

Du kan välja att använda standardbeteenden för annonser.

Så här använder du standardbeteenden:

* Om du implementerar din egen `ContentFactory` klass returnerar du en ny instans av `DefaultAdPolicySelector` i implementeringen av `doRetrieveAdPolicySelector`.

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

* Om du inte har någon anpassad implementering för `ContentFactory` klassen använder TVSDK `DefaultAdPolicySelector`.