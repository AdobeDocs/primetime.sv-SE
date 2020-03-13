---
description: Händelser och meddelanden hjälper dig att hantera de asynkrona aspekterna av videoprogrammet.
seo-description: Händelser och meddelanden hjälper dig att hantera de asynkrona aspekterna av videoprogrammet.
seo-title: Meddelanden och händelser för spelarstatus, aktivitet, fel och loggning
title: Meddelanden och händelser för spelarstatus, aktivitet, fel och loggning
uuid: c4a108e7-72aa-4c96-9538-b1385343d6af
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Meddelanden och händelser för spelarstatus, aktivitet, fel och loggning {#notifications-and-events-for-player-status-activity-errors-and-logging}

Händelser och meddelanden hjälper dig att hantera de asynkrona aspekterna av videoprogrammet.

`MediaPlayerStatus` -objekt ger information om förändringar i spelarstatus. `Notification` -objekt innehåller information om varningar och fel. Fel som stoppar videouppspelningen orsakar också en statusändring för spelaren. Du implementerar händelseavlyssnare för att hämta och svara på händelser ( `MediaPlayerEvent` objekt).

Programmet kan hämta information om meddelanden och status. Med hjälp av den här informationen kan du även skapa ett loggningssystem för diagnostik och validering.

## Meddelandeinnehåll {#section_DF951FF601794CF592841BB7406DC1A1}

`MediaPlayerNotification` innehåller information som är relaterad till spelarens status.

TVSDK tillhandahåller en kronologisk lista över `MediaPlayerNotification` meddelanden och varje meddelande innehåller följande information:

* En tidsstämpel
* Diagnostiska metadata som består av följande element:

   * `type`: INFORMATION, VARNING eller FEL.
   * `code`: En numerisk representation av anmälan.
   * `name`: En beskrivning av meddelandet som kan läsas av människor, till exempel SEEK_ERROR
   * `metadata`: Nyckel-/värdepar som innehåller relevant information om meddelandet. En nyckel med namnet `URL` ger till exempel ett värde som är en URL som är relaterad till meddelandet.

   * `innerNotification`: En referens till ett annat `MediaPlayerNotification` objekt som direkt påverkar det här meddelandet.

Du kan lagra informationen lokalt för senare analys eller skicka den till en fjärrserver för loggning och grafisk representation.

## Konfigurera meddelandesystemet {#section_9E37C09ECFA54B3DA8D3AA9ED1BAFC17}

Du kan lyssna efter meddelanden.

Kärnan i Primetime Players meddelandesystem är `Notification` klassen, som representerar ett fristående meddelande.

Lyssna efter meddelanden så här om du vill få meddelanden:

1. Implementera `NotificationEventListener.onNotification()` återanropet.
1. TVSDK skickar ett `NotificationEvent` objekt till återanropet.

   >[!NOTE]
   >
   >Meddelandetyper räknas upp i `Notification.Type` uppräkningen:

   * `ERROR`
   * `INFO`
   * `WARNING`

## Lägg till loggning och felsökning i realtid {#section_9D4004308CB243AD9B50818895D10005}

Du kan använda meddelanden för att implementera loggning i realtid i videoprogrammet.

Med meddelandesystemet kan du samla in loggnings- och felsökningsinformation för diagnostik och validering utan att behöva stressa systemet.

>[!IMPORTANT]
>
>Återloggningen är inte en del av en produktionskonfiguration och förväntas inte hantera trafik med hög belastning. Om implementeringen inte behöver vara helt fullständig bör du tänka på hur effektiv dataöverföringen är för att undvika att överbelasta systemet.

Här följer ett exempel på hur du hämtar meddelanden:

1. Skapa en timerbaserad körningstråd för videoprogrammet som regelbundet frågar efter data som samlats in av TVSDK-meddelandesystemet.
1. Om timerns intervall är för stort och händelselistans storlek är för liten, kommer meddelandehändelselistan att flöda över.

   >[!NOTE]
   >
   >Gör något av följande för att undvika detta spill:    >
   >    
   >    
   >    1. Minska tidsintervallet som styr tråden som avfrågar efter nya händelser.
   >    1. Öka storleken på meddelandelistan.


1. Serialisera de senaste meddelandehändelseposterna i JSON-format och skicka posterna till en fjärrserver för efterbearbetning.

   >[!NOTE]
   >
   >Fjärrservern kan grafiskt visa angivna data i realtid.

1. Om du vill identifiera förlust av meddelandehändelser ska du leta efter luckor i sekvensen med händelseindexvärden.