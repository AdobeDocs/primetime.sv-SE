---
description: Du kan lyssna efter meddelanden och lägga till egna meddelanden i meddelandehistoriken.
seo-description: Du kan lyssna efter meddelanden och lägga till egna meddelanden i meddelandehistoriken.
seo-title: Konfigurera meddelandesystemet
title: Konfigurera meddelandesystemet
uuid: 2d1876c7-4ce6-491c-880b-dd94697d4feb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---


# Konfigurera meddelandesystemet{#set-up-your-notification-system}

Du kan lyssna efter meddelanden och lägga till egna meddelanden i meddelandehistoriken.

Kärnan i Primetime Players meddelandesystem är klassen Notification, som representerar ett fristående meddelande.

Klassen NotificationHistory innehåller en mekanism för att samla in meddelanden. Den lagrar en logg med meddelandeobjekt ( `NotificationHistoryItem`) som representerar en samling meddelanden.

Så här tar du emot meddelanden:

* Lyssna efter meddelanden
* Lägg till meddelanden i meddelandehistoriken

1. Lyssna efter tillståndsändringar.
1. Implementera händelseavlyssnaren `MediaPlayer.StatusChangeEvent.STATUS_CHANGED`.
1. TVSDK skickar en `MediaPlayer.StatusChangeEvent`-instans till händelseavlyssnaren, som innehåller två parametrar:

   * Det nya läget ( `MediaPlayer.Status`)
   * Ett `MediaPlayerNotification`-objekt

