---
title: Lägg till annonsering
description: Lägg till annonsering
copied-description: true
exl-id: 72f875ea-80ae-482b-94be-41116fff3614
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---

# Lägg till annonsering {#add-advertising}

1. Definiera reklammetadata.

   ```js
   var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
     auditudeSettings.domain = "auditude.com"; 
     auditudeSettings.mediaId = "adbe_tearsofsteel2"; 
     auditudeSettings.zoneId = "123869";
   ```

1. Lägg till annonsmetadata i `MediaResource`.

   ```js
   var mediaResource =  
     new AdobePSDK.MediaResource(resourceUrl, resourceType, auditudeSettings, false);
   ```

1. Lägg till inställningarna i konfigurationen och lägg till en `SpliceOut` parserfabrik.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings; 
   config.advertisingFactory = new ExtCueOutContentFactory(auditudeSettings);
   ```

1. Lägg till `ExtCueOutContentFactory` till biblioteksavsnittet.
1. Ladda ned `ExtCueOutContentFactory.js` från bibliotekssektionen och placera den i arbetsmappen.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script> 
   <script src= "ExtCueOutContentFactory.js"></script>
   ```

1. Testa konfigurationen.
