---
description: Stöd för attributet withCredentials i XMLHttpRequests tillåter resursdelningsbegäranden mellan ursprung (CORS) att inkludera måldomänens cookies för en mängd olika typer av begäranden.
keywords: CORS;cross origin;resource sharing;cookies;withCredentials
seo-description: Stöd för attributet withCredentials i XMLHttpRequests tillåter resursdelningsbegäranden mellan ursprung (CORS) att inkludera måldomänens cookies för en mängd olika typer av begäranden.
seo-title: Resursdelning mellan olika ursprung
title: Resursdelning mellan olika ursprung
uuid: e788b542-d4ac-48aa-91e2-1e88068cbba1
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Resursdelning mellan olika ursprung {#cross-origin-resource-sharing}

Stöd för attributet withCredentials i XMLHttpRequests tillåter resursdelningsbegäranden mellan ursprung (CORS) att inkludera måldomänens cookies för en mängd olika typer av begäranden.

När klienten begär ett manifest, segment eller en nyckel kan servern ange en cookie som klienten måste skicka för efterföljande begäranden. För att tillåta att cookies läses och skrivs måste klienten ange attributet `withCredentials` till `true` för korsorigo begäranden.

Så här aktiverar du stöd `withCredentials` för de flesta typer av begäranden när en viss medieresurs spelas:

1. Skapa `CORSConfig` objektet.

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. Koppla `corsConfig` till `NetworkConfiguration` objektet och ange `useCookieHeaderForAllRequests` till `true`.

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. Anges `networkConfig` i `MediaPlayerItemConfig` objektet.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. Skicka `MediaPlayerItemConfig` till `MediaPlayer.replaceCurrentResource` metoden.

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>Flaggan `useCookieHeaderForAllRequests` påverkar inte licensbegäranden. Om du vill ställa in attributet `withCredentials` för en licensbegäran måste du ange `true` attributet i dina skyddsdata eller ange en auktoriseringsnyckel `withCredentials` `httpRequestHeaders` i skyddsuppgifterna. Exempel:

```
# Example 1 
{ 
    "com.widevine.alpha": {  
        "withCredentials":true,  
        "serverURL":  
          "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=[YOUR_TOKEN</i]" } 
} 
 
# Example 2 
{ 
    "com.widevine.alpha": { 
        "httpRequestHeaders": {  
            "authorization": "true"  
            }, 
        "serverURL":  
          "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=[YOUR_TOKEN</i>]" }
        } 
}
```

Flaggan påverkar inte en licensbegäran eftersom vissa servrar har angett jokertecken (*) som `Access-Control-Allow-Origin` fält i svaret. Men när flaggan för autentiseringsuppgifter är inställd på `true`kan jokertecknet inte användas i `Access-Control-Allow-Origin`. Om du ställer in `useCookieHeaderForAllRequests` på `true` för alla typer av förfrågningar kan du se följande fel för en licensförfrågan:

Kom ihåg följande information:

* När ett anrop med `withCredentials=true` fel misslyckas försöker webbläsaren TVSDK att ringa anropet utan `withCredentials`.
* När ett anrop görs med `networkConfiguration.useCookieHeaderForAllRequests=false`görs XHR-förfrågningar utan `withCredentials` attributet.