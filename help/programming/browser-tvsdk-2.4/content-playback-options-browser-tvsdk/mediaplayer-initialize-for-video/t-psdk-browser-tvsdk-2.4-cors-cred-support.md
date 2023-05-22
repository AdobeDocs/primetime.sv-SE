---
description: Stöd för attributet withCredentials i XMLHttpRequests tillåter resursdelningsbegäranden mellan ursprung (CORS) att inkludera måldomänens cookies för en mängd olika typer av begäranden.
keywords: CORS;korsorigo;resursdelning;cookies;withCredentials
title: Resursdelning mellan olika ursprung
exl-id: 02826c87-b0c6-495b-a17d-67c5693a9772
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Resursdelning mellan olika ursprung {#cross-origin-resource-sharing}

Stöd för attributet withCredentials i XMLHttpRequests tillåter resursdelningsbegäranden mellan ursprung (CORS) att inkludera måldomänens cookies för en mängd olika typer av begäranden.

När klienten begär ett manifest, segment eller en nyckel kan servern ange en cookie som klienten måste skicka för efterföljande begäranden. Klienten måste ange `withCredentials` attribut till `true` för förfrågningar om korsursprung.

Aktivera `withCredentials` stöd för de flesta typer av begäranden när en viss medieresurs spelas upp:

1. Skapa `CORSConfig` -objekt.

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. Bifoga `corsConfig` till `NetworkConfiguration` objekt och ange `useCookieHeaderForAllRequests` till `true`.

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. Ange `networkConfig` i `MediaPlayerItemConfig` -objekt.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. Pass `MediaPlayerItemConfig` till `MediaPlayer.replaceCurrentResource` -metod.

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>The `useCookieHeaderForAllRequests` -flaggan påverkar inte licensförfrågningar. Så här anger du `withCredentials` attribut till `true` för en licensförfrågan måste du ange `withCredentials` i dina skyddsdata eller ange en auktoriseringsnyckel i `httpRequestHeaders` av dina skyddsdata. Till exempel:

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

Flaggan påverkar inte en licensförfrågan eftersom vissa servrar har angett `Access-Control-Allow-Origin` fält till jokertecken (&#39;&#42;&#39;) i sitt svar. Men när inloggningsflaggan är inställd på `true`kan jokertecknet inte användas i `Access-Control-Allow-Origin`. Om du anger `useCookieHeaderForAllRequests` till `true` för alla typer av förfrågningar kan följande fel uppstå för en licensförfrågan:

Kom ihåg följande information:

* När ett samtal med `withCredentials=true` misslyckas, webbläsaren TVSDK försöker ringa om utan `withCredentials`.
* När ett samtal görs med `networkConfiguration.useCookieHeaderForAllRequests=false`, görs XHR-förfrågningar utan `withCredentials` -attribut.
