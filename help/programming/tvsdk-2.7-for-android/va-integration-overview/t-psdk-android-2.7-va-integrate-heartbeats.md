---
title: Initiera och konfigurera videoanalys
description: Initiera och konfigurera videoanalys
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Initiera och konfigurera videoanalys {#initialize-and-configure-video-analytics}

Du kan konfigurera spelaren så att den spårar och analyserar videoanvändningen.
Innan du aktiverar videospårning (videohjärtslag) bör du kontrollera att du har följande:

* TVSDK 2.5 för Android.
* Konfigurations-/initieringsinformation

  Kontakta din Adobe-representant för att få specifik information om ditt videospårningskonto:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json </span> </td> 
   <td colname="col2"> <p>Viktigt: Det här JSON-konfigurationsfilnamnet måste finnas kvar <span class="filepath"> ADBMobileConfig.json </span>. Det går inte att ändra namnet och sökvägen för den här konfigurationsfilen. Sökvägen till filen måste vara <span class="filepath"> &lt;source root=""&gt;/assets </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Slutpunkt för serverspårning av AppMeasurement </td> 
   <td colname="col2"> URL:en för Adobe Analytics-slutsamlingens slutpunkt (tidigare SiteCatalyst). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Serverslutpunkt för videoanalysspårning </td> 
   <td colname="col2"> URL:en för videoanalysens back-end-samlingens slutpunkt. Här skickas alla anrop till spårning av pulsslag. <p>Tips! URL:en för besökarspårningsservern är densamma som URL:en för analysspårningsservern. Information om hur du implementerar tjänsten för besöks-ID finns i <a href="https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en" format="html" scope="external"> Tjänst för implementerings-ID </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Kontonamn </td> 
   <td colname="col2"> Kallas även Report Suite-ID (RSID). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marketing Cloud organisation-ID </td> 
   <td colname="col2"> Ett strängvärde som krävs för att instansiera Visitor-komponenten. </td> 
  </tr> 
 </tbody> 
</table>

Så här konfigurerar du videospårning i spelaren:

1. Bekräfta alternativen för inläsning i dialogrutan `ADBMobileConfig.json` resursfilen är korrekt.

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


   1. Bekräfta att `ADBMobileConfig.json` filen innehåller lämpliga värden (tillhandahålls av Adobe).
   1. Bekräfta att filen finns i `assets/` mapp.

      Mappen måste finnas i roten för programkällträdet.

   1. Kompilera och skapa programmet.
   1. Distribuera och kör det paketerade programmet.

      Mer information om AppMeasurementen finns i [Mäta video i Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=en).

1. Initiera och konfigurera metadata för spårning av pulsslag.

   >[!IMPORTANT]
   >
   >Du kan stoppa videoanalysmodulen mitt i strömmen och återinitiera den om det behövs. Innan modulen initieras om måste du se till att metadata för videoanalys även uppdateras till rätt metadata för innehållet. Om du vill återskapa metadata upprepar du de två första stegen nedan (delsteg) **a** och **b**).

   1. Skapa en instans av metadata för videoanalys.

      Den här instansen innehåller all konfigurationsinformation som behövs för att aktivera spårning av pulsslag för video. Till exempel:

      ```java
      private VideoAnalyticsMetadata getVideoAnalyticsTrackingMetadata() { 
          VideoAnalyticsMetadata vaMetadata = new VideoAnalyticsMetadata(); 
      
          vaMetadata.setTrackingServer("example.com"); 
          vaMetadata.setChannel("test-channel"); 
          vaMetadata.setVideoName("myvideo"); 
          vaMetadata.setVideoId("myvideoid"); 
          vaMetadata.setPlayerName("PSDK Player"); 
          vaMetadata.setUseSSL(false); 
          vaMetadata.debugLogging = true; // Set to NO for production deployment. 
          vaMetadata.setEnableChapterTracking(true); 
          // use this API to override the default asset length -1 for live streams 
          vaMetadata.setAssetDuration(SAMPLE_ASSET_DURATION); 
      
          return vaMetadata; 
      }
      ```

   1. Initiera Video Analytics-providern.

      När du har skapat en mediespelarinstans måste du skapa en Video Analytics-providerinstans och ange programkontexten för den.

      >[!TIP]
      >
      >Skapa alltid en ny providerinstans för varje innehållsuppspelningssession och ta bort den tidigare referensen när du har kopplat från mediespelarinstansen.

      ```java
      VideoAnalyticsProvider videoAnalyticsProvider = new VideoAnalyticsProvider(appContext); 
      ```

   1. Ange metadata för videoanalys på `videoAnalyticsProvider` -instans.

      ```java
      videoAnalyticsProvider.setVideoAnalyticsMetadata(vaMetadata);
      ```

   1. Koppla mediespelarinstansen till `videoAnalyticsProvider` instans:

      ```java
      videoAnalyticsProvider.attachMediaPlayer(mediaPlayer); 
      ```

   1. Förstör Video Analytics-providern.

      Innan du påbörjar en ny innehållsuppspelningssession ska du förstöra den tidigare instansen av videoprovidern. När du har tagit emot händelsen complete (eller meddelandet) väntar du några minuter innan du förstör providerinstansen för videoanalys. Om instansen förstörs omedelbart kan det påverka Video Analytics-providerns möjlighet att skicka en&quot;video complete&quot;-ping.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.detachMediaPlayer(); 
          videoAnalyticsProvider = null; 
      }
      ```

   1. Markera Live-/Linear-strömmen manuellt som slutförd.

      Om du har olika avsnitt i ett direktflöde kan du manuellt markera ett avsnitt som fullständigt med det fullständiga API:t. Detta avslutar videospårningssessionen för det aktuella videoavsnittet och du kan starta en ny spårningssession för nästa avsnitt.

      >[!TIP]
      >
      >Detta API är valfritt och fungerar inte för VOD-videospårning.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.trackVideoComplete();    
      }
      ```
