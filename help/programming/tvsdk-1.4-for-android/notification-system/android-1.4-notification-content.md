---
description: MediaPlayerNotification-objekt innehåller information om ändringar i spelartillstånd, varningar och fel. Fel som stoppar videouppspelningen orsakar också en ändring av spelarens tillstånd.
title: Meddelandeinnehåll
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# Meddelandeinnehåll {#notification-content}

MediaPlayerNotification-objekt innehåller information om ändringar i spelartillstånd, varningar och fel. Fel som stoppar videouppspelningen orsakar också en ändring av spelarens tillstånd.

Programmet kan hämta information om meddelanden och tillstånd. Du kan också skapa ett loggningssystem för diagnostik och validering genom att använda meddelandeinformationen.

Du implementerar händelseavlyssnare för att hämta och svara på händelser. Många evenemang `MediaPlayerNotification` statusmeddelanden.

`MediaPlayerNotification` innehåller information som är relaterad till spelarens status.

TVSDK tillhandahåller en kronologisk lista med `MediaPlayerNotification` meddelanden. Varje anmälan innehåller följande information:

* Tidsstämpel
* Diagnostiska metadata som består av följande element:

   * `type`: INFO, VARNING eller FEL.
   * `code`: En numerisk representation av meddelandet.
   * `name`: En läsbar beskrivning av meddelandet, till exempel SEEK_ERROR
   * `metadata`: Nyckel-/värdepar som innehåller relevant information om meddelandet. En nyckel med namnet `URL` tillhandahåller ett värde som är en URL som är relaterad till meddelandet.

   * `innerNotification`: En referens till en annan `MediaPlayerNotification` objekt som direkt påverkar detta meddelande.

Du kan lagra informationen lokalt för senare analys eller skicka den till en fjärrserver för loggning och grafisk representation.

## Konfigurera meddelandesystemet {#set-up-your-notification-system}

Du kan lyssna efter meddelanden och lägga till egna meddelanden i meddelandehistoriken.

Kärnan i Primetimes meddelandesystem är `Notification` -klass, som representerar ett fristående meddelande.

The `NotificationHistory` -klassen erbjuder en mekanism för att samla in meddelanden. Den lagrar en logg med meddelandeobjekt (NotificationHistoryItem) som representerar en samling meddelanden.

Så här tar du emot meddelanden:

* Lyssna efter meddelanden
* Lägg till meddelanden i meddelandehistoriken

1. Lyssna efter tillståndsändringar.
1. Implementera `MediaPlayer.PlaybackEventListener.onStateChanged` återanrop.
1. TVSDK skickar två parametrar till återanropet:

   * Det nya läget ( `MediaPlayer.PlayerState`)
   * A `MediaPlayerNotification` object

## Lägg till loggning och felsökning i realtid {#add-real-time-logging-and-debugging}

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

   Varje meddelandehändelse har ett indexvärde som automatiskt ökas av `session.NotificationHistory` klassen.

## ID3-taggar {#id-tags}

ID3-taggar ger information om en ljud- eller videofil, till exempel filens titel eller namnet på artisten. TVSDK identifierar ID3-taggar på segmentnivån för transportströmmen (TS) i HLS-strömmar och skickar en händelse. Programmet kan extrahera data från taggen.

>[!IMPORTANT]
>
>TVSDK känner igen ID3-metadata (version 2.3.0 eller 2.4.0) i ljud- (AAC) och videoströmmar (H.264) i någon av dess möjliga kodningar (ASCII, UTF8, UTF16-BE eller UTF16-LE). Den ignorerar ID3-taggar som inte finns i någon av de godkända versionerna eller formaten. Ospecificerad kodning behandlas som UTF8.

När TVSDK identifierar ID3-metadata skickas ett meddelande med följande data:

* InfoCode = 303007
* TYPE = ID3
* NAME = finns inte
* ID = 0

1. Implementera en händelseavlyssnare för `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` och registrera det med `MediaPlayer` -objekt.

   TVSDK anropar den här avlyssnaren när ID3-metadata identifieras.

   >[!NOTE]
   >
   >Anpassade annonser använder samma `onTimedMetadata` -händelse för att indikera identifiering av en ny tagg. Detta bör inte skapa någon förvirring eftersom anpassade annonser identifieras på manifestnivå och ID3-taggar bäddas in i strömmen. Mer information finns i custom-tags-configure.

1. Hämta metadata.

   ```java
   @Override 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       TimedMetadata.Type type = timedMetadata.getType(); 
       if (type.equals(TimedMetadata.Type.ID3)){ 
           long time = timeMetadata.getTime(); 
           Metadata metadata = timedMetadata.getMetadata(); 
           Set<String> keys = metadata.keySet(); 
           for (String key : keys){ 
               String value = metadata.getValue(key); 
           } 
       } 
   }
   ```
