---
description: Du kan lyssna efter meddelanden och lägga till egna meddelanden i meddelandehistoriken.
title: Konfigurera meddelandesystemet
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# Konfigurera meddelandesystemet{#set-up-your-notification-system}

Du kan lyssna efter meddelanden och lägga till egna meddelanden i meddelandehistoriken.

Kärnan i Primetime Players meddelandesystem är klassen `Notification`, som representerar ett fristående meddelande.

Klassen `NotificationHistory` innehåller en mekanism för att samla in meddelanden. Den lagrar en logg med meddelandeobjekt (NotificationHistoryItem) som representerar en samling meddelanden.

Så här tar du emot meddelanden:

* Lyssna efter meddelanden
* Lägg till meddelanden i meddelandehistoriken

1. Lyssna efter tillståndsändringar.
1. Implementera `MediaPlayer.PlaybackEventListener.onStateChanged`-återanropet.
1. TVSDK skickar två parametrar till återanropet:

   * Det nya läget ( `MediaPlayer.PlayerState`)
   * Ett `MediaPlayerNotification`-objekt

