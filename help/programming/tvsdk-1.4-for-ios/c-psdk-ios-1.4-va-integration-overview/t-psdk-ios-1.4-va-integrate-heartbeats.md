---
description: Du kan konfigurera spelaren så att den spårar och analyserar videoanvändningen.
title: Initiera och konfigurera videoanalys
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---


# Initiera och konfigurera videoanalys{#initialize-and-configure-video-analytics}

Du kan konfigurera spelaren så att den spårar och analyserar videoanvändningen.

Innan du aktiverar videospårning (videohjärtslag) bör du kontrollera att du har följande:

* TVSDK för iOS
* Konfigurations-/initieringsinformation - Kontakta din Adobe-representant för att få specifik information om ditt videospårningskonto:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json  </span> </td> 
   <td colname="col2"> <p>Viktigt:  Det här JSON-konfigurationsfilnamnet måste vara <span class="codeph"> ADBMobleConfig.json </span>. Det går inte att ändra namnet och sökvägen för den här konfigurationsfilen. Sökvägen till den här filen måste vara <span class="codeph"> &lt;källrot&gt;/AdobeMobile </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> Slutpunkt  </span> för AppMeasurement Tracking-server </td> 
   <td colname="col2"> URL:en för Adobe Analytics (tidigare SiteCatalyst) back-end-samlingens slutpunkt. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Serverslutpunkt för videoanalysspårning </td> 
   <td colname="col2"> URL:en för videoanalysens back-end-samlingens slutpunkt. Här skickas alla anrop till spårning av pulsslag. <p>Tips:  URL:en för besökarspårningsservern är densamma som URL:en för analysspårningsservern. Mer information om hur du implementerar tjänsten för besöks-ID finns i <a href="https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html" format="html" scope="external"> Implementerings-ID Service </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Kontonamn </td> 
   <td colname="col2"> Kallas även Report Suite-ID (RSID). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marketing Cloud organisation-ID </td> 
   <td colname="col2"> Ett strängvärde som krävs för att instansiera Visitor-komponenten. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Utgivare </td> 
   <td colname="col2"> Detta är utgivar-ID, som tillhandahålls kunderna av deras Adobe-representant. <p>Tips:  Detta ID är inte bara en sträng med varumärkets/tv-namnet. </p> </td> 
  </tr> 
 </tbody> 
</table>

Så här konfigurerar du videospårning i spelaren:

1. Kontrollera att alternativen för inläsning i resursfilen `ADBMobileConfig.json` är korrekta.

   ```
   { 
       "version" : "1.1", 
       "analytics" : { 
           "rsids" : "adobedevelopment", 
           "server" : "10.131.129.149:3000", 
           "charset" : "UTF-8", 
           "ssl" : false, 
           "offlineEnabled" : false, 
           "lifecycleTimeout" : 5, 
           "batchLimit" : 50, 
           "privacyDefault" : "optedin", 
           "poi" : [] 
       }, 
       "marketingCloud": { 
           "org": "ADOBE PROVIDED VALUE"  
       }, 
       "target" : { 
           "clientCode" : "", 
           "timeout" : 5 
       }, 
       "audienceManager" : { 
           "server" : "" 
       } 
   }
   ```

   Den här JSON-formaterade konfigurationsfilen paketeras som en resurs med TVSDK. Spelaren läser endast dessa värden vid inläsningen och värdena förblir konstanta medan programmet körs.

   Så här konfigurerar du inläsningsalternativ:

   1. Bekräfta att filen `ADBMobileConfig.json` innehåller rätt värden från Adobe.
   1. Kontrollera att filen finns i mappen `AdobeMobile`.

      Mappen måste finnas i roten för programkällträdet.
   1. Kompilera och skapa programmet.
   1. Distribuera och kör det paketerade programmet.

      Mer information om de här AppMeasurement-inställningarna finns i [Mäta video i Adobe Analytics](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/).
1. Initiera och konfigurera metadata för spårning av pulsslag.

   >[!IMPORTANT]
   >
   >Du kan stoppa videoanalysmodulen mitt i strömmen och återinitiera den om det behövs. Innan modulen initieras om måste du se till att metadata för videoanalys även uppdateras till rätt metadata för innehållet. Om du vill återskapa metadata upprepar du delstegen 1 och 2.

   1. Skapa en instans av metadata för videoanalys.

      Den här instansen innehåller all konfigurationsinformation som behövs för att aktivera spårning av pulsslag för video. Exempel:

      ```
      - (PTVideoAnalyticsTrackingMetadata *)getVideoAnalyticsTrackingMetadata 
      { 
          PTVideoAnalyticsTrackingMetadata *vaTrackingMetadata =  
            [[[PTVideoAnalyticsTrackingMetadata alloc]  
                 initWithTrackingServer:@"example.com" 
                 publisher:@"sample-publisher"] autorelease]; 
      
          // Set these to NO for production deployment. 
          vaTrackingMetadata.debugLogging = YES;  
          vaTrackingMetadata.quietMode = NO; 
      
          vaTrackingMetadata.channel = @"test-channel"; 
          vaTrackingMetadata.videoName = @"myvideo"; 
          vaTrackingMetadata.videoId = @"myvideoid"; 
          vaTrackingMetadata.playerName = @"PSDK Player"; 
          vaTrackingMetadata.enableChapterTracking = YES; 
          vaTrackingMetadata.useSSL = NO; 
          // use this API to override the default asset length -1 for live streams 
          vaTrackingMetadata.assetDuration = SAMPLE_ASSET_DURATION; 
      
      }
      ```

   1. Lägg till metadata för videoanalys i den globala metadatainstansen.

      När du är klar anger du den globala metadatainstansen för medieresursen eller mediespelarobjektet:

      ```
      - (PTMetadata *)createMetadata 
      { 
          PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
      
          [metadata setMetadata:[self getVideoAnalyticsTrackingMetadata]  
            forKey:PTVideoAnalyticsTrackingMetadataKey]; 
      
          return metadata; 
      } 
      
      PTMetadata *metadata = [self createMetadata]; 
      
      PTMediaPlayerItem *item =  
        [[[PTMediaPlayerItem alloc] initWithUrl:[[[NSURL alloc]  
          initWithString:@"media-url"] autorelease] 
          mediaId:@"media-id" metadata:metadata] autorelease];
      ```

   1. Initiera spåraren för videoanalys.

      När du har skapat en mediespelarinstans måste du skapa en Video Analytics-spårningsinstans och ange en referens till mediespelarinstansen.

      >[!TIP]
      >
      >Skapa alltid en ny spårningsinstans för varje innehållsuppspelningssession och ta bort den tidigare referensen när du har kopplat från mediespelarinstansen.

      ```
      self.videoAnalyticsTracker =  
        [[[PTVideoAnalyticsTracker alloc] initWithMediaPlayer:self.player] autorelease];
      ```

   1. Förstör spårningen av videoanalys.

      Innan du påbörjar en ny innehållsuppspelningssession ska du förstöra den tidigare instansen av videospåraren. När du har tagit emot händelsen complete (eller meddelandet) väntar du några minuter innan du förstör videospårarinstansen. Om instansen förstörs omedelbart kan det påverka möjligheten för Video Analytics-spåraren att skicka en video med fullständig ping.

      ```
      self.videoAnalyticsTracker = nil;
      ```

   1. Markera Live-/Linear-strömmen manuellt som slutförd.

      Om du har olika avsnitt i ett direktflöde kan du manuellt markera ett avsnitt som fullständigt med det fullständiga API:t. Detta avslutar videospårningssessionen för det aktuella videoavsnittet och du kan starta en ny spårningssession för nästa avsnitt.

      >[!TIP]
      >
      >Detta API är valfritt och behövs inte för VOD-videospårning.

      ```
      if (self.videoAnalyticsTracker) 
      { 
         [self.videoAnalyticsTracker trackVideoComplete];   
      }
      ```

