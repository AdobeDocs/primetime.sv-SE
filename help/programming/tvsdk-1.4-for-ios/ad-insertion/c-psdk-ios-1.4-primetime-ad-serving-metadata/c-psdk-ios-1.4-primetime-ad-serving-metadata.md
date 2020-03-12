---
description: TVSDK stöder lösning och infogning av annonser för VOD och live/linear streams.
seo-description: TVSDK stöder lösning och infogning av annonser för VOD och live/linear streams.
seo-title: Metadata för Primetime och server
title: Metadata för Primetime och server
uuid: 314f14c0-4da4-4da6-96f9-5a5ffea22a99
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Översikt {#primetime-ad-server-metadata-overview}

TVSDK stöder lösning och infogning av annonser för VOD och live/linear streams.

>[!NOTE] {othertype=&quot;Prequired&quot;}
>
>Innan du kan inkludera annonser i videoinnehållet måste du ange följande metadatainformation:
>
>* A, `mediaID`som identifierar det specifika innehåll som ska spelas upp.
>* Din `zoneID`, som identifierar ditt företag eller din webbplats.
>* Din annonsserverdomän, som anger domänen för den tilldelade annonsservern.
>* Andra parametrar för målinriktning.
>



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

## Aktivera annonser i repriser vid helhändelse {#section_6016E1DAF03645C8A8388D03C6AB7571}

Full-event replay (FER) är en VOD-resurs som fungerar som en live/DVR-resurs, så programmet måste vidta åtgärder för att se till att annonserna placeras på rätt sätt.

För direktsänt innehåll använder TVSDK metadata/cues i manifestet för att avgöra var annonserna ska placeras. Ibland liknar dock direktsänt eller linjärt innehåll VOD-innehåll. När det aktiva innehållet är klart läggs till exempel en `EXT-X-ENDLIST` tagg till i det aktiva manifestet. För HLS betyder taggen att `EXT-X-ENDLIST` strömmen är en VOD-ström. TVSDK kan inte automatiskt skilja den här strömmen från en vanlig VOD-ström för att korrekt infoga annonser.

Programmet måste informera TVSDK om innehållet är live eller VOD genom att ange `PTAdSignalingMode`.

För en FER-ström bör Adobe Primetime-annonsservern inte innehålla en lista över annonsbrytningar som måste infogas på tidslinjen innan uppspelningen startar. Detta är den typiska processen för VOD-innehåll. Om du anger ett annat signeringsläge läser TVSDK i stället alla referenspunkter från FER-manifestet och går till annonsservern för varje referenspunkt för att begära en annonsbrytning. Den här processen liknar live-/DVR-innehåll.

Förutom varje begäran som är associerad med en referenspunkt gör TVSDK en extra annonsbegäran för annonser före rullning.

1. Hämta det signeringsläge som ska användas från en extern källa, till exempel vCMS.
1. Skapa reklamrelaterade metadata.
1. Om standardbeteendet måste skrivas över anger du `PTAdSignalingMode` med `PTAdMetadata.signalingMode`.

   Giltiga värden är `PTAdSignalingModeDefault`, `PTAdSignalingModeManifestCues`och `PTAdSignalingModeServerMap`.

   Du måste ange annonssignaleringsläget innan du anropar `prepareToPlay`. När TVSDK börjar matcha och placera annonser på tidslinjen ignoreras ändringar av annonseringssigneringsläget. Ange läge när du skapar annonsmetadata för resursen.

1. Fortsätt till uppspelningen.

   ```
      PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.zoneId = your-auditude-zone-id; 
   adMetadata.domain = @"your-auditude-domain"; 
   //adMetadata.enableDVRAds = YES; // FOR LIVE DVR case 
   //adMetadata.signalingMode = PTAdSignalingModeManifestCues;  
   // FOR VOD FER case 
   NSMutableDictionary *targetingParameters = [[[NSMutableDictionary alloc] init] autorelease]; 
   [targetingParameters setValue:@"ipad" forKey:@"device"]; 
   [targetingParameters setValue:@"preroll" forKey:@"AD_OPPORTUNITY_ID"]; 
   adMetadata.targetingParameters = targetingParameters; 
   NSMutableDictionary *customParameters = [[[NSMutableDictionary alloc] init] autorelease]; 
   [customParameters setValue:@"your-media-id" forKey:@"NW_ID"]; 
   [customParameters setValue:@"preroll" forKey:@"AD_OPPORTUNITY_ID"]; 
   adMetadata.customParameters = customParameters; 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   ```

