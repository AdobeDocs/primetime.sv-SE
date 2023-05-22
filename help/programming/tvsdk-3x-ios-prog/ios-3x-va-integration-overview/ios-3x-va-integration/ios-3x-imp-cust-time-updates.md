---
description: I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den position som rapporteras av TVSDK:s localTime-värde. Under en linjär direktuppspelning kan till exempel varje programs spelhuvud anges i förhållande till dess starttid.
title: Implementera anpassade tidsuppdateringar
exl-id: df35d422-d9dc-496d-8f6f-cf34d82ab046
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Implementera anpassade tidsuppdateringar {#implement-custom-time-updates}

I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den position som rapporteras av TVSDK:s localTime-värde. Under en linjär direktuppspelning kan till exempel varje programs spelhuvud anges i förhållande till dess starttid.

>[!TIP]
>
>Åsidosätt bara den här metoden om du vill ange en annan spelhuvudposition än standardpositionen.

Så här åsidosätter du spelhuvudets standardposition:

```
vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
    NSInteger random = arc4random() % 500;  
    return CMTimeMakeWithSeconds(random, 1); 
};
```

>[!IMPORTANT]
>
>I det här kodexemplet är 500 bara ett samplingsvärde. Du måste använda ett annat värde för den anpassade spelhuvudet.
