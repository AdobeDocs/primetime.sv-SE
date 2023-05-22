---
description: Om du vill implementera FairPlay-strömning i din TVSDK-app måste du skriva en Resource Loader, som skickar en licensinhämtningsbegäran till FairPlay-servern.
title: Apple FairPlay i TVSDK-program
exl-id: 83fdc75b-f736-4091-ab80-e7f6e9723482
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# Apple FairPlay i TVSDK-program  {#apple-fairplay-in-tvsdk-applications}

Om du vill implementera FairPlay-strömning i din TVSDK-app måste du skriva en Resource Loader, som skickar en licensinhämtningsbegäran till FairPlay-servern.

Resursinläsarkoden ansvarar för följande åtgärder:

1. Bestäm var förfrågan om licensköp ska skickas.
1. Formatera förfrågan.
1. Ange nödvändig information till servern så att servern kan avgöra om begäran ska tillåtas.

Om du till exempel använder Adobe Primetime Cloud DRM som drivs av ExpressPlay skickar din Resource Loader begäran till:

```
https://fp-gen.service.expressplay.com
```

Resursinläsaren formaterar begäran och kopplar en ExpressPlay-token som tillåter uppspelning till URL:en. När du hämtar ExpressPlay-token finns det flera alternativ att tänka på. Dessa alternativ bestäms av hur du paketerade ditt innehåll.

När du paketerar innehållet infogar paketeraren `skd:` URL:er i ditt M3U8-manifest. Efter `skd:` kan du lägga in alla data i manifestet. Du kan använda dessa data i programkoden för att slutföra de uppgifter som anges ovan. Du kan till exempel använda `skd:{content_id}` så att appen kan avgöra ID:t för det innehåll som spelas upp och begära en token för det specifika innehållet. Du kan till exempel också använda `skd:{entitlement_server_url}?cid={content_id}`så att ditt program inte behöver ha en URL för tillståndsservern hårdkodad.

Du behöver kanske ingen information i `skd:` URL om du redan känner till innehålls-ID via andra kanaler när uppspelningen startar. Det andra exemplet är en perfekt lösning för att testa konfigurationen, men du kan också använda den i en produktionsmiljö.

>[!TIP]
>
>Du bestämmer formatet för `skd:`.

Ditt innehåll hämtas med `skd:` protokoll, men din licensförfrågan använder `https:`. De vanligaste alternativen för att hantera dessa protokoll är:

* **Inledande testning av uppspelning från början till slut** När du paketerar ditt innehåll väljer du en `skd:` URL. När du testar din app måste du hämta en licens från ExpressPlay manuellt och hårdkoda licensen (en `https:` URL) och innehålls-URL i inläsaren.

   Till exempel:

   ```
   NSString* const PLAYLIST_URL =  
     @"https://{your_content_URL}/{your_manifest}.m3u8"; 
   NSString* const EXPRESSPLAY_TOKEN =  
     @"https://fp.service.expressplay.com:80/hms/fp/rights/? 
       ExpressPlayToken={copy_your_token_to_here}";
   ```

* **De flesta andra fallen** När du paketerar ditt innehåll väljer du en `skd:` URL som unikt representerar innehållets ID. I inläsaren tolkar du `skd:` URL, skicka den till servern för att hämta en token och använd den resulterande token som URL.

   Till exempel:

   ```
   - (BOOL)resourceLoader:(AVAssetResourceLoader *)resourceLoader  
         shouldWaitForLoadingOfRequestedResource:(AVAssetResourceLoadingRequest *)loadingRequest { 
       NSURL *url = [[loadingRequest request] URL]; 
       if (![[url scheme] isEqual:@"skd"]) 
           return NO; 
   
       NSString *strUrl = [url absoluteString]; 
       NSLog(@"url is: %@", strUrl); 
   
       strUrl = [strUrl stringByReplacingOccurrencesOfString:@"skd://" withString:@"https://"]; 
   
       NSData *assetId; 
   
       NSData *requestBytes; 
       NSError* error = nil; 
       BOOL handled = NO; 
   
       NSData  *responseData = nil; 
   
       assetId = getMyAssetIdentifierFromURL(url); 
   
       /* Usecase 1: "On Premise Fairplay Server" 
        * Set the strUrl to the OnPremise Fairplay Server Url. The OnPremise Fairplay  
        * Server Url is either hardcoded in the App or derived from strUrl. 
        */ 
   #if 0  
       // Insert your use case 1 codes here: 
       // strUrl = getOnPremiseServerUrl(strUrl, assetId); 
   #endif // 
   
       /* Usecase 2: The strUrl is the entitlement server. 
        * Send assetId to the entitlement server; if the user is allowed to playback  
        * the content, the entitlement server will send back an ExpressPlay Token Url. 
        */ 
   
   #if 0 
       // The hardcoded SEES server: 
       strUrl = @"https://10.0.248.85:8080/sees/SEESServlet"; 
   
       // You can use the following code to simulate a device binding entitlement  
       // request:  
       // First, invoke getExpressPlayTokenUrlFromEntilementServer with  
       // bEnforceDeviceID set to false. When you play the content, the device_id  
       // will be registered on the ExpressPlay Server.  Now change code to set  
       // bEnforceDeviceID to true, and rerun the program. The ExpressPlay token  
       // sent back by the SEES server will be device bound. 
   
       // The strUrl returned below is the ExpressPlay Token URL. 
       strUrl = getExpressPlayTokenUrlFromEntilementServer(strUrl, assetId, true, &error); 
   #endif 
   
       /* Usecase 3: The strUrl is already the ExpressPlay Token Url. 
        */ 
   
       // Read in the certificate 
       NSLog(@"Get Application Certificate"); 
       NSString* certPath = [[NSBundle mainBundle] pathForResource:@"my_certificate.cer"  
                                                            ofType:nil]; 
   
       NSData *appCert = [NSData dataWithContentsOfFile:certPath]; 
   
       // To create the request blob for the server: 
       requestBytes = [loadingRequest streamingContentKeyRequestDataForApp: appCert 
                                                         contentIdentifier:assetId  
                                                                   options:nil  
                                                                     error:&error]; 
       if (requestBytes == nil) { 
           NSLog(@"Error creating server request: %@", error); 
           return false; 
       } 
       // Per the specification, send requestBytes along with the assetId to the Key 
       // Server and obtain the response. 
       NSError *err; 
   
       responseData = getCKCFromExpressPlayService( strUrl, requestBytes, assetId, &err); 
   
       if (responseData != nil) { 
           NSLog(@"Get response data: "); 
           [loadingRequest finishLoadingWithResponse:nil  
                                                data:(NSData *)responseData 
                                            redirect:nil]; 
       } 
       else { 
           [loadingRequest finishLoadingWithError:err]; 
           NSLog(@"bad key response"); 
       } 
       handled = YES; 
   bail: 
       return handled; 
   
   }
   ```

## Aktivera Apple FairPlay i TVSDK-program{#enable-apple-fairplay-in-tvsdk-applications}

Du kan implementera Apple FairPlay Streaming, som är Apple DRM-lösning, i dina TVSDK-program.

1. Skapa en FairPlay-inläsare för kundresurser genom att implementera `PTAVAssetResourceLoaderDelegate`.

   Mer information finns i [Apple FairPlay i TVSDK-program](../../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

   >[!NOTE]
   >
   >Se till att du följer instruktionerna i *FairPlay Streaming Program Guide* ( *FairPlayStreaming_PG.pdf*), som ingår i [FairPlay Server SDK för utveckling av en app som är kompatibel med FPS](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)).

   The `resourceLoader:shouldWaitForLoadingOfRequestedResource` -metoden motsvarar vad som finns i `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT]
   >
   >Om du vill spela upp innehåll ändrar du URL-schemat i din licensbegäran för ExpressPlay-servern från i ExpressPlay-serverscenariot `skd://` till `https://` (eller `https://`).

1. Registrera *FairPlay* Kundresursinläsare med `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

Om du har skrivit en egen FairPlay-licensserver, eller om du använder en tredjepartsserver för FairPlay, kontaktar du licensserverleverantören för att fastställa licensserverns URL, formatering och andra krav.
