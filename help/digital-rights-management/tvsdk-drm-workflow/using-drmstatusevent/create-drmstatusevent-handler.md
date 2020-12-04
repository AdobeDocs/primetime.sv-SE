---
seo-title: Skapa en DRMStatusEvent-hanterare
title: Skapa en DRMStatusEvent-hanterare
uuid: 64f539d9-344c-4372-88b8-c8d098af9dd8
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc
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

