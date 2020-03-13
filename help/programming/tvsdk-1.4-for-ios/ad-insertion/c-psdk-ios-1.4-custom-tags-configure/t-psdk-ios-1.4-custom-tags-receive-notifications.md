---
description: Implementera lämpliga meddelandeavlyssnare om du vill få meddelanden om taggar i manifestet.
seo-description: Implementera lämpliga meddelandeavlyssnare om du vill få meddelanden om taggar i manifestet.
seo-title: Lägg till avlyssnare för tidsbestämda metadataaviseringar
title: Lägg till avlyssnare för tidsbestämda metadataaviseringar
uuid: dcd1bd92-0617-4eab-8b06-7301aaff42f3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Lägg till avlyssnare för tidsbestämda metadataaviseringar {#add-listeners-for-timed-metadata-notifications}

Implementera lämpliga meddelandeavlyssnare om du vill få meddelanden om taggar i manifestet.

Du kan övervaka tidsbestämda metadata genom att avlyssna följande händelser som meddelar programmet om relaterade aktiviteter:

* `PTTimedMetadataChangedNotification`: Varje gång en unik prenumerationstagg identifieras under tolkningen av innehållet förbereder TVSDK ett nytt `PTTimedMetadata` objekt och skickar det här meddelandet.

   Objektet innehåller namnet på taggen som du prenumererar på, lokal tid i uppspelningen där taggen ska visas samt andra data.

* `PTMediaPlayerTimeChangeNotification` : För live-/linjära strömmar där manifestet/spellistan uppdateras regelbundet kan ytterligare anpassade taggar visas i den uppdaterade spellistan/manifestfilen, så ytterligare `TimedMetadata` objekt kan läggas till i `MediaPlayerItem.timedMetadata` egenskapen.

   Den här händelsen meddelar programmet när detta händer.

   Hämta tidsmetadata på något av följande sätt.

   * Ange att programmet ska lägga till sig självt som avlyssnare till `PTTimedMetadataChangedNotification` meddelandet och hämta objektet med `PTTimedMetadataKey`.

      ```
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
        name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
      
      - (void) onTimedMetadataChanged:(NSNotification *) notification { 
          NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
          PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
      }
      ```

   * Få åtkomst till egenskapen `timedMetadataCollection` för `PTMediaPlayerItem`, som består av alla `PTTimedMetadata` objekt som har anmälts hittills.

