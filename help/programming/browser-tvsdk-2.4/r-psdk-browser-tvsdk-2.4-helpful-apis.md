---
description: Det finns vissa API:er som kan hjälpa dig att använda Adobe Flash Player.
seo-description: Det finns vissa API:er som kan hjälpa dig att använda Adobe Flash Player.
seo-title: Användbara API:er för Adobe Flash Player
title: Användbara API:er för Adobe Flash Player
uuid: eae314c0-fd9e-480f-ae1c-9b5f3eb4db4b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Användbara API:er för Adobe Flash Player{#helpful-apis-for-the-adobe-flash-player}

Det finns vissa API:er som kan hjälpa dig att använda Adobe Flash Player.

## AdobePSDK.MediaResource {#section_8C339FA1386D4B1A926A1459B2619E5E}

```js
new MediaResource(url, type, metadata, forceFlash)
```

Om det stöds kan du använda parametern `forceFlash` för att åsidosätta bestämningssekvensen för uppspelningstekniken och tvinga implementeringen att använda Flash Player.

<!--<a id="section_FEE3205B532446498771F7DD55B5E79F"></a>-->

```js
AdobePSDK.PlayerTechnology = { 
/** 
* Determine the {AdobePSDK.PlayerTechnology} that would be used for the given 
* media resource. 
* @param {AdobePSDK.MediaResource} mediaResource 
* @returns {AdobePSDK.PlayerTechnology.Type} 
*/ 
getSupportedTechnology(mediaResource); 
}; 
 
AdobePSDK.PlayerTechnology.Type = {  
MSE, 
VIDEO_TAG,  
FLASH,  
UNKNOWN 
}; 
 
/** 
* Set the path to the SWF relative to the main html page or using http URL. 
* Defaults to the current directory of the html page. 
* 
* @param swfPath 
*/ 
AdobePSDK.setSWFPath(swfPath); 
 
/** 
* Set the path to the folder containing the authorization token(s). 
* If not set, defaults to the token folder within the SWFPath: SWFPath + "token/". 
* @param authorizationTokenPath 
*/ 
AdobePSDK.setAuthorizationTokenPath(authorizationTokenPath); 
 
/** 
* Set the name of the authorization token file. Defaults to "hlsAF_localhost.dat". 
* @param authorizationTokenFileName 
*/ 
AdobePSDK.setAuthorizationTokenFilename(authorizationTokenFilename); 
 
/** 
* Set the authorization token type, can be "SWF" or "DAT". Defaults to "DAT" 
* @param {String} authorizationTokenType 
*/ 
AdobePSDK.setAuthorizationTokenType(authorizationTokenType);
```

