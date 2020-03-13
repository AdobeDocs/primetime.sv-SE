---
description: I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den position som rapporteras av Browser TVSDK localTime-värdet.
seo-description: I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den position som rapporteras av Browser TVSDK localTime-värdet.
seo-title: Implementera anpassade tidsuppdateringar
title: Implementera anpassade tidsuppdateringar
uuid: 26a0592c-a47b-4d65-b984-5e51533dcddc
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Implementera anpassade tidsuppdateringar{#implement-custom-time-updates}

I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den position som rapporteras av Browser TVSDK localTime-värdet.

Under en linjär direktuppspelning kan till exempel varje programs spelhuvud anges i förhållande till dess starttid.

>[!TIP]
>
>Åsidosätt bara den här metoden om du vill ange en annan spelhuvudposition än standardpositionen.

Så här åsidosätter du spelhuvudets standardposition:

```js
vaMetadata.currentTimeUpdateBlock = function() { 
       return playerPositionInSeconds; 
}; 
```

>[!IMPORTANT]
>
>Värdena i det här kodfragmentet är bara exempel. Du måste använda olika värden för den anpassade spelhuvudspositionen.

