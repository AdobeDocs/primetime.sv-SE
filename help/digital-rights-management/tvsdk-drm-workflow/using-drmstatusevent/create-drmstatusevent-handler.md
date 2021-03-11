---
title: Skapa en DRMStatusEvent-hanterare
description: Skapa en DRMStatusEvent-hanterare
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# Skapa en DRMStatusEvent-hanterare{#create-a-drmstatusevent-handler}

I följande exempel skapas en händelsehanterare som returnerar DRM-innehållets statusinformation för det Primetime-objekt som händelsen härstammar från.

Lägg till en händelsehanterare i ett Primetime-objekt som pekar på skyddat innehåll:

```
function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
```

