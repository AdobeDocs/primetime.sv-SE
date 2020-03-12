---
description: 'null'
seo-description: 'null'
seo-title: Lägg till annonsering
title: Lägg till annonsering
uuid: 7762506f-b55e-445d-b8a2-c1208358a370
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Lägg till annonsering {#add-advertising}

1. Definiera reklammetadata.

   ```js
   var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
     auditudeSettings.domain = "auditude.com"; 
     auditudeSettings.mediaId = "adbe_tearsofsteel2"; 
     auditudeSettings.zoneId = "123869";
   ```

1. Lägg till reklammetadata i `MediaResource`.

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

1. Lägg till filen `ExtCueOutContentFactory` i biblioteksavsnittet.
1. Hämta filen `ExtCueOutContentFactory.js` från bibliotekssektionen och placera den i arbetsmappen.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script> 
   <script src= "ExtCueOutContentFactory.js"></script>
   ```

1. Testa konfigurationen.
