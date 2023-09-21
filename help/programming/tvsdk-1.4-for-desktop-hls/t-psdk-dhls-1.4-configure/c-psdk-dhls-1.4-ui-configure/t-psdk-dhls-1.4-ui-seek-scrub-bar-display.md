---
description: TVSDK har stöd för sökning till en viss position (tid) där strömmen är en spelningslista med skjutbara fönster, i både VOD (video on demand) och liveströmmar.
title: Visa ett söknavigeringsfält med aktuell uppspelningsposition
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Visa ett söknavigeringsfält med aktuell uppspelningsposition{#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK har stöd för sökning till en viss position (tid) där strömmen är en spelningslista med skjutbara fönster, i både VOD (video on demand) och liveströmmar.

>[!IMPORTANT]
>
>Sökning i en liveström är endast tillåtet för DVR.

1. Konfigurera återanrop för sökning.

       Sökningen är asynkron, så TVSDK skickar följande sökrelaterade händelser:
   
   * `SeekEvent.SEEK_BEGIN` - Sök efter start.
   * `SeekEvent.SEEK_END` - Sökningen lyckades.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` - ändrade sökpositionen som användaren angett.

1. Vänta tills spelaren har en giltig status för sökning.

   Giltiga lägen är FÖRBEREDDA, SLUTFÖRDA, PAUSED och PLAYING.

1. Lyssna efter lämplig händelse för att se när användaren drar.
1. Skicka den begärda sökpositionen (millisekunder) till `MediaPlayer.seek` -metod.

   ```
   function seek(position:Number):void;
   ```

   Du kan bara söka efter resursens sökbara längd. För video on demand är längden från 0 till dess resursens varaktighet.

   >[!TIP]
   >
   >Detta flyttar spelhuvudet till en ny position i strömmen, men den slutliga beräknade positionen kan skilja sig från den angivna sökpositionen.

1. Vänta på att TVSDK skickar `SeekEvent.SEEK_END` -händelse.
1. Hämta den slutliga justerade uppspelningspositionen med event.actualPosition.

       Detta är viktigt eftersom den faktiska startpositionen efter sökningen kan skilja sig från den begärda positionen. Olika regler kan gälla, bland annat:
   
   * Uppspelningsbeteendet påverkas om en sökning eller annan omplacering slutar mitt i en annonsbrytning eller hoppar över annonsbrytningar.
   * Om du söker nära en segmentgräns justeras sökpositionen till början av segmentet.

1. Använd positionsinformationen när du visar en sökningslist.
