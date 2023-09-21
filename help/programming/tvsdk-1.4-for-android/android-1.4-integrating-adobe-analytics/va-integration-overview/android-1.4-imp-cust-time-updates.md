---
description: I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den position som rapporteras av TVSDK:s localTime-värde. Under en linjär direktuppspelning kan till exempel varje programs spelhuvud anges i förhållande till dess starttid.
title: Implementera anpassade tidsuppdateringar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Implementera anpassade tidsuppdateringar {#implement-custom-time-updates}

I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den position som rapporteras av TVSDK:s localTime-värde. Under en linjär direktuppspelning kan till exempel varje programs spelhuvud anges i förhållande till dess starttid.

>[!TIP]
>
>Åsidosätt bara den här metoden om du vill ange en annan spelhuvudposition än standardpositionen.

Så här åsidosätter du spelhuvudets standardposition:

```java
vaMetadata.setCurrentTimeUpdateBlock(new VideoAnalyticsMetadata.CurrentTimeUpdateBlock() { 
    @Override 
    public long call() { 
        long range = 500L; 
        Random r = new Random() 
        return (long)(r.nextDouble()*range); 
    } 
});
```

>[!IMPORTANT]
>
>Värdena i det här kodfragmentet är bara exempel. Du måste använda olika värden för den anpassade spelhuvudspositionen.
