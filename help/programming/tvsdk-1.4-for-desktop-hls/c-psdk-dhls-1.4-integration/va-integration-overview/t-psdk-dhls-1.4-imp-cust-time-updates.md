---
description: I vissa analysimplementeringar kanske klientprogrammet vill ange en annan spelhuvudposition än den som rapporteras av TVSDK localTime-värdet. Under en LINEAR-direktuppspelning kan till exempel varje programs spelhuvud anges i förhållande till dess starttid.
title: Implementera anpassade tidsuppdateringar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

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
