---
description: Du kan lyssna efter meddelanden och lägga till egna meddelanden i meddelandehistoriken.
seo-description: Du kan lyssna efter meddelanden och lägga till egna meddelanden i meddelandehistoriken.
seo-title: Konfigurera meddelandesystemet
title: Konfigurera meddelandesystemet
uuid: caa6a306-dea9-45ee-b0b3-569b5f2527a1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '132'
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

