---
description: Du kan lyssna efter meddelanden och lägga till egna meddelanden i meddelandehistoriken.
title: Konfigurera meddelandesystemet
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
