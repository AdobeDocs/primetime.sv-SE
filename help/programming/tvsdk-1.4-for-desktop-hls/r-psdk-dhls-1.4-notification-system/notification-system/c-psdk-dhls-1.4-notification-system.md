---
description: MediaPlayerNotification-objekt innehåller information om ändringar i spelarstatus, varningar och fel. Fel som stoppar videouppspelningen orsakar också en statusändring för spelaren.
title: Meddelanden om spelarstatus, aktivitet, fel och loggning
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# Översikt {#notifications-for-player-status-activity-errors-and-logging-overview}

MediaPlayerNotification-objekt innehåller information om ändringar i spelarstatus, varningar och fel. Fel som stoppar videouppspelningen orsakar också en statusändring för spelaren.

Programmet kan hämta information om meddelanden och status. Du kan också skapa ett loggningssystem för diagnostik och validering genom att använda meddelandeinformationen.

Du implementerar händelseavlyssnare för att hämta och svara på händelser. Många händelser ger `MediaPlayerNotification` statusmeddelanden.