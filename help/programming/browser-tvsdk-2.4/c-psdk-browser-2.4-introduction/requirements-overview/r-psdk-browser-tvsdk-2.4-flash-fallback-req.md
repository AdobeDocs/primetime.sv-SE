---
description: Om du vill använda Flash Player måste du kontrollera att miljön uppfyller de nödvändiga kraven.
seo-description: Om du vill använda Flash Player måste du kontrollera att miljön uppfyller de nödvändiga kraven.
seo-title: Krav för Flash Player
title: Krav för Flash Player
uuid: f181457b-2bb4-4baa-b2b7-d787f65fab75
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Krav för Flash Player{#flash-player-requirements}

Om du vill använda Flash Player måste du kontrollera att miljön uppfyller de nödvändiga kraven.

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

Här följer kraven för Flash Player:

* Om du vill spela upp med `Primetime.js`måste du installera minst Flash Player version 23.
* Installera minst Flash Player version 11.0.0 om du vill bli tillfrågad om uppdateringar av Flash Player version 23 eller senare.

## Förpackningskrav {#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

För uppspelning med Flash Player krävs följande SWF-filer:

* Den huvudsakliga SWF-programfilen som hanterar webbläsar-TVSDK-API:er.
* Den `playerProductInstall.swf` SWF-fil som hanterar installation och uppdatering av Flash Player.

Dessutom kräver videouppspelning i Flash en auktoriseringstokenfil som kan vara en SWF-fil eller en `.DAT` fil. Sökvägen till SWF-filerna, auktoriseringstokenfilen samt tokenfilens namn och typ kan anges med API:erna för AdobePSDK.

Exempel:

```js
// Set relative or http path to directory containing SWF.  
// Defaults to current directory for the html page. 
AdobePSDK.setSWFPath(<swfPath>); 
 
// Set the relative or http path to directory containing token file(s). 
// Defaults to SWFPath + "token/". 
AdobePSDK.setAuthorizationTokenPath(<authorizationTokenPath>); 
 
// Set the name of the token file, do not include any path in this string. 
AdobePSDK.setAuthorizationTokenFilename("hlsaf_localhost.swf"); 
 
//Set the token type, "DAT" or "SWF". Defaults to "DAT" 
AdobePSDK.setAuthorizationTokenType("SWF");
```

