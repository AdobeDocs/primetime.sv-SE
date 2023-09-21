---
description: MediaPlayerStatus-objekt innehåller information om förändringar i spelarstatus. Meddelandeobjekt innehåller information om varningar och fel. Fel som stoppar videouppspelningen orsakar också en statusändring för spelaren. Du implementerar händelseavlyssnare för att hämta och svara på händelser (MediaPlayerEvent-objekt).
title: Meddelanden och händelser för spelarstatus, aktivitet, fel och loggning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# Meddelanden och händelser för spelarstatus, aktivitet, fel och loggning {#notifications-and-events-for-player-status-activity-errors-and-logging}

Händelser och meddelanden hjälper dig att hantera de asynkrona aspekterna av videoprogrammet.

MediaPlayerStatus-objekt innehåller information om förändringar i spelarstatus. Meddelandeobjekt innehåller information om varningar och fel. Fel som stoppar videouppspelningen orsakar också en statusändring för spelaren. Du implementerar händelseavlyssnare för att hämta och svara på händelser (MediaPlayerEvent-objekt).

Programmet kan hämta information om meddelanden och status. Med hjälp av den här informationen kan du även skapa ett loggningssystem för diagnostik och validering.

## Meddelandeinnehåll {#section_DF951FF601794CF592841BB7406DC1A1}

`MediaPlayerNotification` innehåller information som är relaterad till spelarens status.

TVSDK tillhandahåller en kronologisk lista med `MediaPlayerNotification` meddelanden och varje meddelande innehåller följande information:

* En tidsstämpel
* Diagnostiska metadata som består av följande element:

   * `type`: INFO, VARNING eller FEL.
   * `code`: En numerisk representation av meddelandet.
   * `name`: En läsbar beskrivning av meddelandet, till exempel SEEK_ERROR
   * `metadata`: Nyckel-/värdepar som innehåller relevant information om meddelandet. En nyckel med namnet `URL` tillhandahåller ett värde som är en URL som är relaterad till meddelandet.

   * `innerNotification`: En referens till en annan `MediaPlayerNotification` objekt som direkt påverkar detta meddelande.

Du kan lagra informationen lokalt för senare analys eller skicka den till en fjärrserver för loggning och grafisk representation.

## Konfigurera meddelandesystemet {#section_9E37C09ECFA54B3DA8D3AA9ED1BAFC17}

Du kan lyssna efter meddelanden.

Kärnan i Primetimes meddelandesystem är `Notification` -klass, som representerar ett fristående meddelande.

Lyssna efter meddelanden så här om du vill få meddelanden:

1. Implementera `NotificationEventListener.onNotification()` återanrop.
1. TVSDK skickar en `NotificationEvent` till återanropet.

   >[!NOTE]
   >
   >Meddelandetyper räknas upp i `Notification.Type` enum:

   * `ERROR`
   * `INFO`
   * `WARNING`

## Lägg till loggning och felsökning i realtid {#section_9D4004308CB243AD9B50818895D10005}

Du kan använda meddelanden för att implementera loggning i realtid i videoprogrammet.

Med meddelandesystemet kan du samla in loggnings- och felsökningsinformation för diagnostik och validering utan att behöva stressa systemet.

>[!IMPORTANT]
>
>Återloggningen är inte en del av en produktionskonfiguration och förväntas inte hantera trafik med hög belastning. Om implementeringen inte behöver vara helt fullständig bör du tänka på hur effektiv dataöverföringen är för att undvika att överbelasta systemet.

Här är ett exempel på hur du hämtar meddelanden:

1. Skapa en timerbaserad körningstråd för videoprogrammet som regelbundet frågar efter data som samlats in av TVSDK-meddelandesystemet.
1. Om timerns intervall är för stort och händelselistans storlek är för liten, kommer meddelandehändelselistan att flöda över.

   >[!NOTE]
   >
   >Gör något av följande för att undvika detta spill:
   >
   >1. Minska tidsintervallet som styr tråden som avfrågar efter nya händelser.
   >1. Öka storleken på meddelandelistan.
   >

1. Serialisera de senaste meddelandehändelseposterna i JSON-format och skicka posterna till en fjärrserver för efterbearbetning.

   >[!NOTE]
   >
   >Fjärrservern kan grafiskt visa angivna data i realtid.

1. Om du vill identifiera förlust av meddelandehändelser ska du leta efter luckor i sekvensen med händelseindexvärden.
