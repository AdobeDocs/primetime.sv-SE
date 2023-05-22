---
description: I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den position som rapporteras av TVSDK-värdet localTime. Under en linjär direktuppspelning kan till exempel varje programs spelhuvud anges i förhållande till dess starttid.
title: Implementera anpassade tidsuppdateringar
exl-id: 91e778ca-cdab-4c50-96f8-3333d210fd4a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Implementera anpassade tidsuppdateringar {#implement-custom-time-updates}

I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den position som rapporteras av TVSDK-värdet localTime. Under en linjär direktuppspelning kan till exempel varje programs spelhuvud anges i förhållande till dess starttid.

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
