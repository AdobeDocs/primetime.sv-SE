---
description: I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den position som rapporteras av TVSDK:s localTime-värde. Under en linjär direktuppspelning kan till exempel varje programs spelhuvud anges i förhållande till dess starttid.
seo-description: I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den position som rapporteras av TVSDK:s localTime-värde. Under en linjär direktuppspelning kan till exempel varje programs spelhuvud anges i förhållande till dess starttid.
seo-title: Implementera anpassade tidsuppdateringar
title: Implementera anpassade tidsuppdateringar
uuid: 303303eb-c371-4766-a1ee-806ba75b4e01
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '190'
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

