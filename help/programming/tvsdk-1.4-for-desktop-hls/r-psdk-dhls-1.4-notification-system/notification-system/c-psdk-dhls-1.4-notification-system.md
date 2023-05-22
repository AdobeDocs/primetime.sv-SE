---
description: MediaPlayerNotification-objekt innehåller information om ändringar i spelarstatus, varningar och fel. Fel som stoppar videouppspelningen orsakar också en statusändring för spelaren.
title: Meddelanden om spelarstatus, aktivitet, fel och loggning
exl-id: cce634aa-5394-46c0-a031-70d6fc1b754b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Översikt {#notifications-for-player-status-activity-errors-and-logging-overview}

MediaPlayerNotification-objekt innehåller information om ändringar i spelarstatus, varningar och fel. Fel som stoppar videouppspelningen orsakar också en statusändring för spelaren.

Programmet kan hämta information om meddelanden och status. Du kan också skapa ett loggningssystem för diagnostik och validering genom att använda meddelandeinformationen.

Du implementerar händelseavlyssnare för att hämta och svara på händelser. Många evenemang `MediaPlayerNotification` statusmeddelanden.
