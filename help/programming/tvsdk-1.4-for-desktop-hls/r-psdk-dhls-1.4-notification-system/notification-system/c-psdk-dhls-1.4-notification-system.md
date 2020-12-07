---
description: MediaPlayerNotification-objekt innehåller information om ändringar i spelarstatus, varningar och fel. Fel som stoppar videouppspelningen orsakar också en statusändring för spelaren.
seo-description: MediaPlayerNotification-objekt innehåller information om ändringar i spelarstatus, varningar och fel. Fel som stoppar videouppspelningen orsakar också en statusändring för spelaren.
seo-title: Meddelanden om spelarstatus, aktivitet, fel och loggning
title: Meddelanden om spelarstatus, aktivitet, fel och loggning
uuid: 7ce5bed0-f312-437e-a82f-b1d4a8e1926c
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# Översikt {#notifications-for-player-status-activity-errors-and-logging-overview}

MediaPlayerNotification-objekt innehåller information om ändringar i spelarstatus, varningar och fel. Fel som stoppar videouppspelningen orsakar också en statusändring för spelaren.

Programmet kan hämta information om meddelanden och status. Du kan också skapa ett loggningssystem för diagnostik och validering genom att använda meddelandeinformationen.

Du implementerar händelseavlyssnare för att hämta och svara på händelser. Många händelser ger `MediaPlayerNotification` statusmeddelanden.