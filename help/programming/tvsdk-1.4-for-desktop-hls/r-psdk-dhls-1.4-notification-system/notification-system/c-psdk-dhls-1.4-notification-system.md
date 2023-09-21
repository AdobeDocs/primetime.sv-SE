---
description: MediaPlayerNotification-objekt innehåller information om ändringar i spelarstatus, varningar och fel. Fel som stoppar videouppspelningen orsakar också en statusändring för spelaren.
title: Meddelanden om spelarstatus, aktivitet, fel och loggning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Ökning {#notifications-for-player-status-activity-errors-and-logging-overview}

MediaPlayerNotification-objekt innehåller information om ändringar i spelarstatus, varningar och fel. Fel som stoppar videouppspelningen orsakar också en statusändring för spelaren.

Programmet kan hämta information om meddelanden och status. Du kan också skapa ett loggningssystem för diagnostik och validering genom att använda meddelandeinformationen.

Du implementerar händelseavlyssnare för att hämta och svara på händelser. Många evenemang `MediaPlayerNotification` statusmeddelanden.
