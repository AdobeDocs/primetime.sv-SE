---
description: I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den som rapporteras av TVSDK localTime-värdet. Under en LINEAR-direktuppspelning kan till exempel varje programs spelhuvud anges i förhållande till dess starttid.
seo-description: I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den som rapporteras av TVSDK localTime-värdet. Under en LINEAR-direktuppspelning kan till exempel varje programs spelhuvud anges i förhållande till dess starttid.
seo-title: Implementera anpassade tidsuppdateringar
title: Implementera anpassade tidsuppdateringar
uuid: 2b46eca9-3815-4c44-ab5e-21678c35f410
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Implementera anpassade tidsuppdateringar{#implement-custom-time-updates}

I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den som rapporteras av TVSDK localTime-värdet. Under en LINEAR-direktuppspelning kan till exempel varje programs spelhuvud anges i förhållande till dess starttid.

>[!TIP]
>
>Åsidosätt bara den här metoden om du vill ange en annan spelhuvudposition än standardpositionen.

1. Så här åsidosätter du spelhuvudets standardposition:

   ```
   vaMetadata.currentTimeUpdateBlock = function():Number { 
      if (currentTime == 0) { 
          currentTime = getTimer(); 
      } 
      return ((getTimer() - currentTime) / 1000 + 1000); 
   }
   ```

   >[!IMPORTANT]
   >
   >Värdena i det här kodfragmentet är bara exempel. Du måste använda olika värden för den anpassade spelhuvudspositionen.

