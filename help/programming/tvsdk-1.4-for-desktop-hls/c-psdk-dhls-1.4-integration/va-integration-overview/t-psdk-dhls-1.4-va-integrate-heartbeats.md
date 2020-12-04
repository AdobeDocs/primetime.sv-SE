---
description: Du kan konfigurera spelaren så att den spårar och analyserar videoanvändningen.
seo-description: Du kan konfigurera spelaren så att den spårar och analyserar videoanvändningen.
seo-title: Initiera och konfigurera videoanalys
title: Initiera och konfigurera videoanalys
uuid: ece5ddc1-3f7b-4878-b1bc-1fec0a459add
translation-type: tm+mt
source-git-commit: 6cb3463be8986d8a1dc718655bd929a0f07ac00d
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---


# Initiera och konfigurera videoanalys{#initialize-and-configure-video-analytics}

Du kan konfigurera spelaren så att den spårar och analyserar videoanvändningen.

Innan du aktiverar videospårning (videohjärtslag) bör du kontrollera att du har följande:

* TVSDK for Desktop HLS
* Konfigurations-/initieringsinformation - Kontakta din Adobe-representant för att få specifik information om ditt videospårningskonto:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> Slutpunkt för AppMeasurement Tracking-server </td> 
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
   <td colname="col1"> Slutpunkt för besöksspårningsserver </td> 
   <td colname="col2"> URL:en för serverslutpunkten som ger en unik identifierare för det aktuella visningsprogrammet. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Utgivare </td> 
   <td colname="col2"> Detta är utgivar-ID, som tillhandahålls kunderna av deras Adobe-representant. <p>Tips:  Detta ID är inte bara en sträng med varumärkets/tv-namnet. </p> </td> 
  </tr> 
 </tbody> 
</table>

Så här konfigurerar du videospårning i spelaren:

1. Instansiera och konfigurera VisitorAPI-biblioteket.

       Tänk på följande:
   
   * Instansieringen kräver en indataparameter för Marketing Cloud organisation-ID som tillhandahålls av Adobe.

      Detta är ett strängvärde.
   * Det enda konfigurationsalternativet för VisitorAPI-biblioteket är URL:en för serverslutpunkten som innehåller den unika identifieraren för den aktuella användaren.
   * URL:en för besökarspårningsservern är densamma som URL:en för analysspårningsservern.

      Information om hur du implementerar Visitor ID-tjänsten finns i Implementering av Visitor ID-tjänst.

   ```
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID"); 
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”; 
   ```

1. Instansiera och konfigurera komponenten AppMeasurement.

   AppMeasurement-instansen har många konfigurationsalternativ. Mer information finns i [dokumentationen för Adobe Analytics Developer](https://microsite.omniture.com/t2/help/en_US/reference/#Developer). Alternativen i följande exempelkod ( `account`, `visitorNamespace` och `trackingServer`) krävs, och värdena tillhandahålls av Adobe.

   >[!IMPORTANT]
   >
   >Du måste se till att beroendekedjan är korrekt konfigurerad. AppMeasurement-instansen aggregerar (är beroende av) Visitor API-komponenten.

   ```
   // Instantiate and configure AppMeasurement 
   
   // Instantiate AppMeasurement instance only once! 
   if (_appMeasurementObject == null) {  
       _appMeasurementObject = new AppMeasurement(); 
   } 
   
   with (_appMeasurementObject) { 
       account = "ACCOUNT_NAME"; // Also known as RSID 
       trackingServer = "URL_OF_THE_ADOBE_ANALYTICS_TRACKING_SERVER"; 
   
       // Use the same value here as for the Visitor API component 
       visitorNamespace = "MARKETING_CLOUD_ORG_ID"; 
   
       // Attach the Visitor API to the AppMeasurement instance. 
       visitor = _visitor;  
       pageName = "pageName"; 
       charSet = "UTF-8"; 
       currencyCode = "USD"; 
   } 
   ```

   >[!IMPORTANT]
   >
   >Kontrollera att `appMeasurementObject.visitor` är ifyllt i programmet innan du startar videoanalysflödet, annars kanske du inte får några spårningsresultat. Dessa resultat indikeras av meddelandena i loggen. Du kan lägga till ett tomt spåranrop ( `appMeasurementObject.track`), avfråga egenskapen `visitor` tills den har fyllts i och starta videoanalys.

1. Initiera och konfigurera metadata för spårning av pulsslag.

   >[!IMPORTANT]
   >
   >Du kan stoppa videoanalysmodulen mitt i strömmen och återinitiera den om det behövs. Innan modulen initieras om måste du se till att metadata för videoanalys även uppdateras till rätt metadata för innehållet. Om du vill återskapa metadata upprepar du delstegen 1 och 2.

   1. Skapa en instans av metadata för videoanalys.

      Den här instansen innehåller all konfigurationsinformation som behövs för att aktivera spårning av pulsslag för video. Exempel:

      ```
      private function getVideoAnalyticsTrackingMetadata():VideoAnalyticsMetadata {     
          // Initialize visitor id service and appMeasurement      
          [...] // as shown in the previous steps     
      
          var vaMetadata:VideoAnalyticsMetadata = new VideoAnalyticsMetadata(); 
      
          with (vaMetadata) { 
              trackingServer = "hbTrackingServer"; 
              publisher = "hbPublisher"; 
              channel = "hbChannel";  
              playerName = "hbPlayerName"; 
      
              // this overwrites the ContextData variable a.media.friendlyName 
              videoName = "hbFriendlyName";  
      
              // this will overwrite the ContextData variable a.media.name 
              videoId = "hbName"; 
      
              enableChapterTracking = true; 
      
              // Set these to false for production deployment 
              debugLogging = true;  
              quietMode = false; 
      
          } 
      } 
      ```

   1. Lägg till metadata för videoanalys i den globala metadatainstansen.

      När du är klar anger du den globala metadatainstansen för medieresursen eller mediespelarobjektet:

      ```
      var resourceMetadata:Metadata = _player.currentItem.resource.metadata; 
      resourceMetadata.setMetadata(DefaultMetadataKeys.VIDEO_ANALYTICS_METADATA_KEY,  
                                   getVideoAnalyticsTrackingMetadata());
      ```

   1. Initiera spåraren för videoanalys.

      När du har skapat en mediespelarinstans måste du skapa en Video Analytics-spårningsinstans och ange en referens till mediespelarinstansen.

      >[!TIP]
      >
      >Skapa alltid en ny spårningsinstans för varje innehållsuppspelningssession och ta bort den tidigare referensen när du har kopplat från mediespelarinstansen.

      ```
      _videoAnalyticsProvider = new VideoAnalyticsProvider(_appMeasurementObject); 
      _videoAnalyticsProvider.attachMediaPlayer(_player);
      ```

   1. Förstör spårningen av videoanalys.

      Innan du påbörjar en ny innehållsuppspelningssession ska du förstöra den tidigare instansen av videospåraren. När du har tagit emot händelsen complete (eller meddelandet) väntar du några minuter innan du förstör videospårarinstansen. Om instansen förstörs omedelbart kan det påverka möjligheten för Video Analytics-spåraren att skicka en video med fullständig ping.

      ```
      if (videoAnalyticsTracker) { 
          videoAnalyticsTracker.detachMediaPlayer(); 
          videoAnalyticsTracker = null; 
      }
      ```

   1. Markera Live-/Linear-strömmen manuellt som slutförd.

      Om du har olika avsnitt i ett direktflöde kan du manuellt markera ett avsnitt som fullständigt med det fullständiga API:t. Detta avslutar videospårningssessionen för det aktuella videoavsnittet och du kan starta en ny spårningssession för nästa avsnitt.

      >[!TIP]
      >
      >Detta API är valfritt och behövs inte för VOD-videospårning.

