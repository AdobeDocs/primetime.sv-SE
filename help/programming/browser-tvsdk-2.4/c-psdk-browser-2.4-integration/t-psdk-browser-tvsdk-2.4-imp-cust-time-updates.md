---
description: I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den position som rapporteras av Browser TVSDK localTime-värdet.
title: Implementera anpassade tidsuppdateringar
exl-id: 4d045c4d-298a-42ae-af61-0463a76bc872
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

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
