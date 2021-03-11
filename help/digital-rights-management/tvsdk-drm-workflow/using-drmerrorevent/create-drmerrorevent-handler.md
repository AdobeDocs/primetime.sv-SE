---
title: Skapa en DRMErrorEvent-hanterare
description: Skapa en DRMErrorEvent-hanterare
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# Skapa en DRMErrorEvent-hanterare{#create-a-drmerrorevent-handler}

Skapa en händelsehanterare för att bearbeta felhändelser som skickas från Primetime när ett fel påträffas när skyddat innehåll spelas upp.

När ett program påträffar ett fel utförs vanligtvis ett antal rensningsåtgärder. Därefter informeras användaren om felet och användaren får alternativ för att lösa problemet.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

