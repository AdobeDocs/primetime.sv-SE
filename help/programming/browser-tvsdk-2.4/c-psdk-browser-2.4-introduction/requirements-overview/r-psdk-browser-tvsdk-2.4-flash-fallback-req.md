---
description: För att kunna använda Flash Player måste du se till att din miljö uppfyller de krav som ställs.
title: Krav för Flash Player
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 1%

---


# Krav för Flash Player{#flash-player-requirements}

För att kunna använda Flash Player måste du se till att din miljö uppfyller de krav som ställs.

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

Här är kraven för Flash Player:

* Om du vill spela upp med `Primetime.js` måste du installera minst Flash Player version 23.
* Installera minst Flash Player version 11.0.0 om du vill bli tillfrågad om uppdateringar av Flash Player version 23 eller senare.

## Paketeringskrav {#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

För uppspelning med Flash Player krävs följande SWF-filer:

* Den huvudsakliga SWF-programfilen som hanterar webbläsar-TVSDK-API:er.
* Den `playerProductInstall.swf` SWF-fil som hanterar installation och uppdateringar av Flash Player.

Dessutom kräver videouppspelning i Flash en auktoriseringstokenfil som kan vara en SWF- eller `.DAT`-fil. Sökvägen till SWF-filerna, auktoriseringstokenfilen samt tokenfilens namn och typ kan anges med API:erna för AdobePSDK.

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

