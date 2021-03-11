---
description: Du kan implementera Apple FairPlay Streaming, som är Apples DRM-lösning, i dina TVSDK-program.
title: Aktivera Apple FairPlay i TVSDK-program
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# Aktivera Apple FairPlay i TVSDK-program{#enable-apple-fairplay-in-tvsdk-applications}

Du kan implementera Apple FairPlay Streaming, som är Apples DRM-lösning, i dina TVSDK-program.

1. Skapa en FairPlay-kundresursinläsare genom att implementera `PTAVAssetResourceLoaderDelegate`.

   Mer information finns i [Apple FairPlay i TVSDK-program](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

   >[!NOTE]
   >
   >Se till att du följer instruktionerna i *FairPlay Streaming Program Guide* ( *FairPlayStreaming_PG.pdf*), som ingår i [FairPlay Server SDK för utveckling av en FPS-kompatibel app](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)).

   Metoden `resourceLoader:shouldWaitForLoadingOfRequestedResource` motsvarar vad som finns i `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT]
   >
   >Om du vill spela upp innehåll i ExpressPlay-licensserverscenariot ändrar du URL-schemat i din licensbegäran för ExpressPlay från `skd://` till `https://` (eller `https://`).

1. Registrera *FairPlay* Customer Resource Loader med `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

Om du har skrivit en egen FairPlay-licensserver, eller om du använder en tredjepartsserver för FairPlay, kontaktar du licensserverleverantören för att fastställa licensserverns URL, formatering och andra krav.
