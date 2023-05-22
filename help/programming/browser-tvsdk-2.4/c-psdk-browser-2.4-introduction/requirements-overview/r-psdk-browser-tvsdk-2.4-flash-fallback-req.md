---
description: För att kunna använda Flash Player måste du se till att din miljö uppfyller de krav som ställs.
title: Krav för Flash Player
exl-id: 26531d0d-d34c-4134-8a05-0604f00a3107
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Krav för Flash Player{#flash-player-requirements}

För att kunna använda Flash Player måste du se till att din miljö uppfyller de krav som ställs.

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

Här är kraven för Flash Player:

* Spela upp med `Primetime.js`, installera minst Flash Player version 23.
* Installera minst Flash Player version 11.0.0 om du vill bli tillfrågad om uppdateringar av Flash Player version 23 eller senare.

## Förpackningskrav {#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

För uppspelning med Flash Player krävs följande SWF-filer:

* Huvudfilen för programmet SWF som hanterar API:er för webbläsarens TVSDK.
* The `playerProductInstall.swf` SWF-fil som hanterar installation och uppdatering av Flash Player.

Dessutom kräver videouppspelning i Flash en auktoriseringstokenfil som kan vara SWF eller en `.DAT` -fil. Sökvägen till SWF-filerna, auktoriseringstokenfilen samt tokenfilens namn och typ kan anges med API:erna för AdobePSDK.

Till exempel:

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
