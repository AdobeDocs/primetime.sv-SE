---
seo-title: Skapa en DRMErrorEvent-hanterare
title: Skapa en DRMErrorEvent-hanterare
uuid: dde660fc-6899-47d4-97d4-46acda2db262
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc
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

