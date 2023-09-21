---
description: I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den position som rapporteras av TVSDK:s localTime-värde. Under en linjär direktuppspelning kan till exempel varje programs spelhuvud anges i förhållande till dess starttid.
title: Implementera anpassade tidsuppdateringar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Implementera anpassade tidsuppdateringar{#implement-custom-time-updates}

I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den position som rapporteras av TVSDK:s localTime-värde. Under en linjär direktuppspelning kan till exempel varje programs spelhuvud anges i förhållande till dess starttid.

>[!TIP]
>
>Åsidosätt bara den här metoden om du vill ange en annan spelhuvudposition än standardpositionen.

1. Så här åsidosätter du spelhuvudets standardposition:

   ```
   vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
       NSInteger random = arc4random() % 500;  
       return CMTimeMakeWithSeconds(random, 1); 
   };
   ```

   >[!IMPORTANT]
   >
   >I det här kodexemplet är 500 bara ett samplingsvärde. Du måste använda ett annat värde för den anpassade spelhuvudet.
