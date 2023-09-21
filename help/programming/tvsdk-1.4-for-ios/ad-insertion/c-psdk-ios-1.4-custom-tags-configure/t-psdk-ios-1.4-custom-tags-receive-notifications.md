---
description: Implementera lämpliga meddelandeavlyssnare om du vill få meddelanden om taggar i manifestet.
title: Lägg till avlyssnare för tidsbestämda metadataaviseringar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Lägg till avlyssnare för tidsbestämda metadataaviseringar {#add-listeners-for-timed-metadata-notifications}

Implementera lämpliga meddelandeavlyssnare om du vill få meddelanden om taggar i manifestet.

Du kan övervaka tidsbestämda metadata genom att avlyssna följande händelser som meddelar programmet om relaterade aktiviteter:

* `PTTimedMetadataChangedNotification`: Varje gång en unik prenumerationstagg identifieras under tolkningen av innehållet förbereder TVSDK en ny `PTTimedMetadata` och skickar det här meddelandet.

  Objektet innehåller namnet på taggen som du prenumererar på, lokal tid i uppspelningen där taggen ska visas samt andra data.

* `PTMediaPlayerTimeChangeNotification` : För live-/linjära strömmar där manifestet/spellistan uppdateras regelbundet kan ytterligare anpassade taggar visas i den uppdaterade spellistan/manifestet, så ytterligare `TimedMetadata` kan läggas till i `MediaPlayerItem.timedMetadata` -egenskap.

  Den här händelsen meddelar programmet när detta händer.

  Hämta tidsmetadata på något av följande sätt.

   * Ange att programmet ska lägga till sig själv som avlyssnare för `PTTimedMetadataChangedNotification` meddela och hämta objektet med `PTTimedMetadataKey`.

     ```
     [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
       name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
     
     - (void) onTimedMetadataChanged:(NSNotification *) notification { 
         NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
         PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
     }
     ```

   * Öppna `timedMetadataCollection` egenskap för `PTMediaPlayerItem`, som består av alla `PTTimedMetadata` objekt som har anmälts hittills.
