---
description: Browser TVSDK har ett DRM-gränssnitt som du kan använda för att spela upp innehåll som skyddas av olika DRM-lösningar, inklusive FairPlay, PlayReady och Widewin.
title: Översikt över DRM-gränssnittet
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Översikt över DRM-gränssnittet{#drm-interface-overview}

Browser TVSDK har ett DRM-gränssnitt som du kan använda för att spela upp innehåll som skyddas av olika DRM-lösningar, inklusive FairPlay, PlayReady och Widewin.

<!--<a id="section_59994F2059B245E996E0776214804A0A"></a>-->

>[!IMPORTANT]
>
>DRM-stöd finns för MPEG-Dash-strömmar som skyddas av Microsoft PlayReady (på Internet Explorer på Windows 8.1 och Edge) och Widewin (på Google Chrome) DRM-system. DRM-stöd finns för HLS-strömmar på Safari som skyddas med FairPlay.

Nyckelgränssnittet för DRM-arbetsflödet är `DRMManager`. En referens till `DRMManager`-instansen kan hämtas via MediaPlayer-instansen:

* `var mediaPlayer = new AdobePSDK.MediaPlayer();`
* `var drmManager = mediaPlayer.drmManager;`

<!--<a id="section_B7E8AD9A4D4F4BD9BA2A67ABC135D6F9"></a>-->

Här är ett arbetsflöde på hög nivå för uppspelning av DRM-skyddat innehåll:

1. Om du vill bifoga DRM-systemspecifika data som ska användas av Browser TVSDK i licensinhämtningsprocessen för en skyddad ström gör du följande anrop innan du anropar `mediaPlayer.replaceCurrentResource`:

   ```js
   var protectionData = { 
       "com.adobe.primetime": { 
          "serverURL": { 
             "individualization-request": "https://individualization.adobe.com/flashaccess/i15n/v5", 
             "license-request": "https://example.com:8096/flashaccess/req", 
             "license-release": "https://example.com:8096/flashaccess/req" 
          }, 
          "httpRequestHeaders": { 
          } 
       } 
   }; 
   var drmManager = mediaPlayer.drmManager; 
   drmManager.setProtectionData(protectionData);
   ```

1. Om samma innehåll förväntas fungera med olika DRM-system i olika webbläsare kan skyddsdata anges för flera DRM-system.

   ```js
   var protectionData = { 
       "com.adobe.primetime": { 
           "serverURL": { 
               "individualization-request": "https://individualization.adobe.com/flashaccess/i15n/v5", 
               "license-request": "https://example.com:8096/flashaccess/req", 
               "license-release": "https://example.com:8096/flashaccess/req" 
           }, 
           "httpRequestHeaders": { 
           } 
       }, 
       "com.widevine.alpha": { 
           "serverURL": "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<token value>", 
           "httpRequestHeaders": { 
               "dt-custom-data": "eyJ1c2VySWQiOiIxMjM0NS" 
           } 
       }, 
       "com.microsoft.playready": { 
           "serverURL": "https://pr.test.expressplay.com/playready/RightsManager.asmx?ExpressPlayToken=<token value>", 
           "httpRequestHeaders": { 
               "http-header-CustomData": "eyJ1c2VySWQiOiIxMjM0NS" 
           } 
       }, 
       "com.apple.fps.1_0": { 
           "serverURL": "https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<token value>", 
           "certificateURL": "Path_To_certificate.cer", 
           "licenseResponseType": "arraybuffer", 
           "httpRequestHeaders": { 
               "Content-type": "application/octet-stream" 
           } 
       }, 
       "org.w3.clearkey": { 
           "clearkeys": { 
               "H3JbV93QV3mPNBKQON2UtQ": "ClKhDPHMtCouEx1vLGsJsA", 
               "IAAAACAAIAAgACAAAAAAAg": "5t1CjnbMFURBou087OSj2w" 
           } 
       } 
   }; 
   
   var drmManager = mediaPlayer.drmManager; 
   drmManager.setProtectionData(protectionData);
   ```

1. När skyddsdata inte är inställda hämtas nödvändig information, t.ex. licens-URL:en, från PSSH-rutan för DRM-system där det är tillämpligt.

   >[!TIP]
   >
   >Om du anger skyddsdata åsidosätts den licens-URL som anges i rutan PSSH.

1. Som standard är sessionstypen för DRM-licensen tillfällig, vilket innebär att licensen inte lagras när sessionen stängs.

   Du kan ange en sessionstyp med hjälp av ett API i `DRMManager`.  För bakåtkompatibilitet är sessionstyperna `temporary`, `persistent-license`, `persistent-usage-record` och `persistent`.

   ```js
   var drmManager = mediaPlayer.drmManager; 
    drmManager.setEMESessionType(“<YOUR_SESSION_TYPE>”); 
   ```

1. När `sessionType` används är `persistent-license` eller `persistent` kan DRM-licensen returneras genom att anropa `DRMManager.returnLicense`.

   ```js
   var onLicenseReturnFunc = function () { 
       console.log("DRM: License Return Complete "); 
   }, 
   
   onLicenseReturnErrorFunc = function (major, minor, errorString/*, errorServerUrl*/) { 
      console.log("DRM: License Return Error: " + errorString); 
   }, 
   
   drmManager = mediaPlayer.drmManager; 
   
   if (drmManager) { 
       var returnLicenseListener = new  
           AdobePSDK.DRMReturnLicenseListener(onLicenseReturnFunc, onLicenseReturnErrorFunc); 
       drmManager.returnLicense(null, null, null, false, returnLicenseListener, drmLicense.session); 
   }
   ```

