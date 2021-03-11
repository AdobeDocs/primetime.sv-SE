---
description: Du kan använda TVSDK för att hämta information om media som du kan visa i sökfältet.
title: Visa videons varaktighet, aktuella tid och återstående tid
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Visa videons varaktighet, aktuella tid och återstående tid{#display-the-duration-current-time-and-remaining-time-of-the-video}

Du kan använda TVSDK för att hämta information om media som du kan visa i sökfältet.

1. Vänta tills spelaren har statusen INITIALIZED.
1. Hämta den aktuella spelhuvudstiden med egenskapen `MediaPlayer.currentTime`.

   Detta returnerar spelhuvudets aktuella position på den virtuella tidslinjen i millisekunder. Tiden beräknas i förhållande till den matchade strömmen som kan innehålla flera instanser av alternativt innehåll, till exempel flera annonser eller annonsbrytningar som delas upp i huvudströmmen. För live-/linjära strömmar är den returnerade tiden alltid i uppspelningsfönsterintervallet.

   ```
   function get currentTime():Number;
   ```

1. Hämta uppspelningsintervallet för strömmen och fastställ varaktigheten.
   1. Använd egenskapen `mediaPlayer.playbackRange` för att hämta tidsintervallet för den virtuella tidslinjen.

      ```
      function get playbackRange():TimeRange;
      ```

   1. Tolka tidsintervallet med `mediacore.utils.TimeRange`.
   1. Ta bort början från intervallets slut om du vill bestämma varaktigheten.

      Detta omfattar längden på ytterligare innehåll som infogas i strömmen (annonser).

      För VOD börjar intervallet alltid med noll och slutvärdet är lika med summan av innehållets längd och varaktigheten för ytterligare innehåll som infogas i flödet (annonser).

      För en linjär/liveresurs representerar intervallet uppspelningsfönstret och det här intervallet ändras under uppspelningen.

      TVSDK skickar en `MediaPlayerItemEvent.ITEM_UPDATED`-händelse som anger att medieobjektet uppdaterades och att dess attribut (inklusive uppspelningsintervallet) uppdaterades.

1. Använd de metoder som är tillgängliga för klassen `MediaPlayer` och klassen `HSlider` som är allmänt tillgänglig i Flex SDK för att ställa in sökfältsparametrarna.

1. Använd en timer för att regelbundet hämta aktuell tid och uppdatera `SeekBar`.
