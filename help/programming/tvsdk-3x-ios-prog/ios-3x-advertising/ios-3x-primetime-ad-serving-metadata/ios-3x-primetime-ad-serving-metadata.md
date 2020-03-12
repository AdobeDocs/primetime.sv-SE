---
description: TVSDK stöder lösning och infogning av annonser för VOD och live/linear streams.
seo-description: TVSDK stöder lösning och infogning av annonser för VOD och live/linear streams.
seo-title: Metadata för Primetime och server
title: Metadata för Primetime och server
uuid: 61e224dd-551a-438f-8560-e64915087fef
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Översikt {#primetime-ad-server-metadata-overview}

TVSDK stöder lösning och infogning av annonser för VOD och live/linear streams.

[!PREREQUISITE] {othertype=&quot;Prequired&quot;}

Innan du kan inkludera annonser i videoinnehållet måste du ange följande metadatainformation:

* A, `mediaID`som identifierar det specifika innehåll som ska spelas upp.
* Din `zoneID`, som identifierar ditt företag eller din webbplats.
* Din annonsserverdomän, som anger domänen för den tilldelade annonsservern.
* Andra parametrar för målinriktning.

## Konfigurera metadata för Primetime och server {#section_86C4A3B2DF124770B9B7FD2511394313}

Ditt program måste förse TVSDK med den information som krävs för att ansluta till annonsservern. `PTAuditudeMetadata`

Så här ställer du in annonsserverns metadata:

1. Skapa en instans av [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) och ange dess egenskaper.

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. Ange `PTAuditudeMetadata` instansen som metadata för aktuella `PTMediaPlayerItem` metadata genom att använda `PTAdResolvingMetadataKey`.

   ```
   // Metadata is an instance of PTMetadata that is used to create the PTMediaPlayerItem 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey];  
   [adMetadata release];
   ```

   Här är ett exempel:

   ```
   PTMetadata *metadata = [self createMetadata]; 
   PTMediaPlayerItem *item =  
     [[[PTMediaPlayerItem alloc] initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease]; 
   
   - (PTMetadata *) createMetadata { 
       PTMetadata* metadata = [[[PTMetadata alloc] init] autorelease]; 
   
       PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease];  
       adMetadata.zoneId = yourZoneID; 
       adMetadata.domain = yourAdServerDomain; 
   
       [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   
       return metadata; 
   }
   ```
