---
description: Du kan lyssna efter meddelanden och lägga till egna meddelanden i meddelandehistoriken.
title: Konfigurera meddelandesystemet
exl-id: da6cec2d-8488-4f61-881b-72999ece650c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Konfigurera meddelandesystemet{#set-up-your-notification-system}

Du kan lyssna efter meddelanden och lägga till egna meddelanden i meddelandehistoriken.

Kärnan i Primetime Players meddelandesystem är klassen Notification, som representerar ett fristående meddelande.

Klassen NotificationHistory innehåller en mekanism för att samla in meddelanden. Den lagrar en logg med meddelanden ( `NotificationHistoryItem`) som representerar en samling meddelanden.

Så här tar du emot meddelanden:

* Lyssna efter meddelanden
* Lägg till meddelanden i meddelandehistoriken

1. Lyssna efter tillståndsändringar.
1. Implementera `MediaPlayer.StatusChangeEvent.STATUS_CHANGED` händelseavlyssnare.
1. TVSDK skickar en `MediaPlayer.StatusChangeEvent` -instans till händelseavlyssnaren som innehåller två parametrar:

   * Det nya läget ( `MediaPlayer.Status`)
   * A `MediaPlayerNotification` object
