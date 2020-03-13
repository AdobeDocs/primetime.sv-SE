---
description: Om du vill implementera FairPlay-strömning i din TVSDK-app måste du skriva en Resource Loader, som skickar en licensinhämtningsbegäran till FairPlay-servern.
seo-description: Om du vill implementera FairPlay-strömning i din TVSDK-app måste du skriva en Resource Loader, som skickar en licensinhämtningsbegäran till FairPlay-servern.
seo-title: Apple FairPlay i TVSDK-applikationer
title: Apple FairPlay i TVSDK-applikationer
uuid: 5796d5af-0018-4c69-a755-65e4819ee838
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Apple FairPlay i TVSDK-applikationer {#apple-fairplay-in-tvsdk-applications}

Om du vill implementera FairPlay-strömning i din TVSDK-app måste du skriva en Resource Loader, som skickar en licensinhämtningsbegäran till FairPlay-servern.

Resursinläsarkoden ansvarar för följande åtgärder:

1. Bestäm var förfrågan om licensköp ska skickas.
1. Formatera förfrågan.
1. Ange nödvändig information till servern så att servern kan avgöra om begäran ska tillåtas.

Om du till exempel använder Adobes Primetime Cloud DRM som drivs av ExpressPlay skickar din Resource Loader begäran till:

```
https://fp-gen.service.expressplay.com
```

Resursinläsaren formaterar begäran och kopplar en ExpressPlay-token som tillåter uppspelning till URL:en. När du hämtar ExpressPlay-token finns det flera alternativ att tänka på. Dessa alternativ bestäms av hur du paketerade ditt innehåll.

När du paketerar ditt innehåll infogar paketeraren URL: `skd:` er i ditt M3U8-manifest. Efter `skd:` inmatningen kan du lägga in alla data i manifestet. Du kan använda dessa data i programkoden för att slutföra de uppgifter som anges ovan. Du kan till exempel använda `skd:{content_id}` så att din app kan avgöra ID:t för det innehåll som spelas upp och begära en token för det specifika innehållet. Du kan till exempel använda `skd:{entitlement_server_url}?cid={content_id}`så att ditt program inte behöver ha en URL för tillståndsservern hårdkodad.

Du behöver kanske ingen information i din `skd:` URL om du redan känner till innehålls-ID via andra kanaler när uppspelningen startar. Det andra exemplet är en perfekt lösning för att testa konfigurationen, men du kan också använda den i en produktionsmiljö.

>[!TIP]
>
>Du bestämmer formatet för `skd:`.

Ditt innehåll hämtas med hjälp av `skd:` protokollet, men din licensbegäran använder `https:`. De vanligaste alternativen för att hantera dessa protokoll är:

* **Inledande testning av uppspelning** från början till slut Välj en `skd:` URL när du paketerar innehållet. När du testar din app måste du hämta en licens från ExpressPlay och hårdkoda licensen (en `https:` URL) och innehålls-URL:en i din inläsare manuellt.

   Exempel:

   ```
   NSString* const PLAYLIST_URL =  
     @"https://{your_content_URL}/{your_manifest}.m3u8"; 
   NSString* const EXPRESSPLAY_TOKEN =  
     @"https://fp.service.expressplay.com:80/hms/fp/rights/? 
       ExpressPlayToken={copy_your_token_to_here}";
   ```

* **De flesta andra fall** När du paketerar innehåll väljer du en `skd:` URL som unikt representerar innehållets ID. Tolka URL-adressen i inläsaren, skicka den till servern för att hämta en token och använd den resulterande token som URL-adress. `skd:`

   Exempel:

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

## Aktivera Apple FairPlay i TVSDK-program {#section_61CFA3C22FE64F52B2C8CE860B72E88B}

Du kan implementera Apple FairPlay Streaming, som är Apples DRM-lösning, i dina TVSDK-program.

1. Skapa en FairPlay-kundresursinläsare genom att implementera `PTAVAssetResourceLoaderDelegate`. Mer information finns i Apple FairPlay i TVSDK-program.

   >[!NOTE]
   >
   >Se till att du följer instruktionerna i *FairPlay Streaming Program Guide* ( *FairPlayStreaming_PG.pdf*), som ingår i [FairPlay Server SDK för utveckling av en FPS-kompatibel app](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)).

   Metoden `resourceLoader:shouldWaitForLoadingOfRequestedResource` motsvarar det som finns i `AVAssetResourceLoaderDelegate`.

   >[!NOTE]
   >
   >Om du vill spela upp innehåll i ExpressPlay-licensserverscenariot ändrar du URL-schemat i din licensbegäran för ExpressPlay-servern från `skd://` till `https://` (eller `https://`).

1. Registrera *FairPlay* Customer Resource Loader med `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

   >[!NOTE]
   >
   >Om du har skrivit en egen FairPlay-licensserver, eller om du använder en tredjepartsserver för FairPlay, kontaktar du licensserverleverantören för att fastställa licensserverns URL, formatering och andra krav.