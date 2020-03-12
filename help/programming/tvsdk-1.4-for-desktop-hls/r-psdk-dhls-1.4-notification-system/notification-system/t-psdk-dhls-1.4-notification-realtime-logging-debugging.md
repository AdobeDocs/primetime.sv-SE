---
description: Du kan använda meddelanden för att implementera loggning i realtid i videoprogrammet.
seo-description: Du kan använda meddelanden för att implementera loggning i realtid i videoprogrammet.
seo-title: Lägg till loggning och felsökning i realtid
title: Lägg till loggning och felsökning i realtid
uuid: 568ea2e7-963b-427e-9cb2-e261e4423902
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Lägg till loggning och felsökning i realtid{#add-real-time-logging-and-debugging}

Du kan använda meddelanden för att implementera loggning i realtid i videoprogrammet.

Med meddelandesystemet kan du samla in loggnings- och felsökningsinformation för diagnostik och validering utan att behöva stressa systemet för mycket.

>[!IMPORTANT]
>
>Återloggningen är inte en del av en produktionskonfiguration och förväntas inte hantera trafik med hög belastning. Om implementeringen inte behöver vara helt fullständig bör du tänka på hur effektiv dataöverföringen är för att undvika att överbelasta systemet.

Här är ett exempel på hur du hämtar meddelanden.

1. Skapa en timerbaserad körningstråd för videoprogrammet som regelbundet frågar efter data som samlats in av TVSDK-meddelandesystemet.

1. Om timerns intervall är för stort och storleken på händelselistan är för liten, kommer meddelandehändelselistan att flöda över. Gör något av följande för att undvika detta spill:

   * Minska tidsintervallet som styr tråden som avfrågar efter nya händelser.
   * Öka storleken på meddelandelistan.

1. Serialisera de senaste meddelandehändelseposterna i JSON-format och skicka posterna till en fjärrserver för efterbearbetning.

   Fjärrservern kan sedan grafiskt visa de data som tillhandahålls i realtid.
1. Om du vill identifiera förlust av meddelandehändelser ska du leta efter luckor i sekvensen med händelseindexvärden.

   Varje meddelandehändelse har ett indexvärde som automatiskt ökas av `NotificationHistory` klassen.
