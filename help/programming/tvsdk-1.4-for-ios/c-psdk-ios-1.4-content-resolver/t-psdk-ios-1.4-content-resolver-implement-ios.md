---
description: Du kan implementera dina lösningar baserat på standardlösare.
title: Implementera en anpassad lösning för affärsmöjlighet/innehåll
exl-id: f2a8512f-9f6c-4fd9-8694-32132cddc7d2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# Implementera en anpassad lösning för affärsmöjlighet/innehåll{#implement-a-custom-opportunity-content-resolver}

Du kan implementera dina lösningar baserat på standardlösare.

<!--<a id="fig_CC41E2A66BDB4115821F33737B46A09B"></a>-->

![](assets/ios_psdk_content_resolver.png)

1. Utveckla en anpassad annonslösare genom att utöka `PTContentResolver` abstrakt klass.

   `PTContentResolver` är ett gränssnitt som måste implementeras av en innehållslösningsklass. En abstrakt klass med samma namn är också tillgänglig och hanterar konfigurationen automatiskt (hämtar delegaten).

   >[!TIP]
   >
   >`PTContentResolver` exponeras genom `PTDefaultMediaPlayerClientFactory` klassen. Klienter kan registrera en ny innehållslösare genom att utöka `PTContentResolver` abstrakt klass. Som standard, och om den inte tas bort specifikt, är en `PTDefaultAdContentResolver` är registrerad i `PTDefaultMediaPlayerClientFactory`.

   ```
   @protocol PTContentResolver <NSObject> 
   @required 
   + (BOOL)shouldHandleOpportunity:(PTPlacementOpportunity *)opportunity;  
   //Detector returns YES/NO if it should handle the following placement opportunity 
   - (void)configWithPlayerItem:(PTMediaPlayerItem *)item  
                 delegate:(id<PTContentResolverDelegate> delegate); 
   - (void)process:(PTPlacementOpportunity *)opportunity; 
   - (void)timeout:(PTPlacementOpportunity *)opportunity;  
   //The timeout method gets invoked if the TVSDK decides that the  
   //PTContentResolver is taking too much time to respond. 
   @end 
   
   @interface PTContentResolver : NSObject <PTContentResolver> 
   
   @property (readonly) id<PTContentResolverDelegate> delegate; 
   @property (readonly) PTMediaPlayerItem *playerItem; 
   
   - (BOOL)shouldHandleOpportunity:(PTPlacementOpportunity *)opportunity; 
   - (void)configWithPlayerItem:(PTMediaPlayerItem *)item  
                  delegate:(id<PTContentResolverDelegate>) delegate; 
   - (void)process:(NSArray *)opportunities; 
   - (void)cancel:(NSArray *)opportunities; 
   @end
   ```

1. Implementera `shouldResolveOpportunity` och returnera `YES` om den ska hantera mottagna `PTPlacementOpportunity`.
1. Implementera `resolvePlacementOpportunity`, som börjar läsa in alternativt innehåll eller annonser.
1. När annonserna har lästs in förbereder du en `PTTimeline` med information om innehållet som ska infogas.

       Nedan finns användbar information om tidslinjer:
   
   * Det kan finnas flera `PTAdBreak`för pre-roll, mid-roll och post-roll.

      * A `PTAdBreak` har följande:

         * A `CMTimeRange` med brytningens starttid och varaktighet.

            Detta anges som intervallegenskapen för `PTAdBreak`.

         * `NSArray` av `PTAd`s.

            Detta anges som egenskapen ads för `PTAdBreak`.
   * A `PTAd` representerar annonsen, och `PTAd` har följande:

      * A `PTAdHLSAsset` anges som primär tillgångsegenskap för annonsen.
      * Möjligen flera `PTAdAsset` instanser som klickbara annonser eller banners.

   Till exempel:

   ```
   NSMutableArray *ptBreaks = [[[NSMutableArray alloc] init] autorelease]; 
   
   // Prepare the primary asset of the ad - links to ad m3u8 
   PTAdHLSAsset *ptAdAsset = [[[PTAdHLSAsset alloc] init] autorelease]; 
   ptAdAsset.source = AD_SOURCE_M3U8; 
   ptAdAsset.id = FAKE_NUMBER_ID; 
   ptAdAsset.format = @"video"; 
   
   // Prepare the ad itself. 
   PTAd *ptAd = [[[PTAd alloc] init] autorelease]; 
   ptAd.primaryAsset = ptAdAsset; 
   ptAd.primaryAsset.ad = ptAd; 
   
   // Prepare the break and add the ad created above. 
   PTAdBreak *ptBreak = [[[PTAdBreak alloc] init] autorelease]; 
   ptBreak.relativeRange = CMTimeRangeMake(BREAK_START_TIME, BREAK_DURATION_VALUE); 
   [ptBreak addAd:ptAd]; 
   
   // Add the break to array of breaks. 
   [ptBreaks addObject:adBreak]; 
   
   // Once all breaks have been prepared, they can be set on timeline 
   PTTimeline *_timeline = [[PTTimeline alloc] init]; 
   _timeline.adBreaks = ptBreaks;
   ```

1. Utlysning `didFinishResolvingPlacementOpportunity`, som innehåller `PTTimeline`.
1. Registrera din anpassade content/ad resolver till standardmediespelarfabriken genom att ringa `registerContentResolver`.

   ```
   //Remove default content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearContentResolvers]; 
   
   //Create an instance of your content/ad resolver (id <PTContentResolver>) 
   CustomContentResolver *contentResolver = [[CustomContentResolver alloc] init]; 
   
   //Set custom content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] registerContentResolver:[contentResolver autorelease]];
   ```

1. Om du har implementerat en anpassad lösning för affärsmöjlighet registrerar du den i standardfabriken för mediespelare.

   >[!TIP]
   >
   >Du behöver inte registrera en anpassad lösning för affärsmöjlighet för att registrera en anpassad lösning för innehåll/annonser.

   ```
   //Remove default opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearOpportunityResolvers]; 
   
   //Create an instance of your opportunity resolver (id <PTOpportunityResolver>) 
   CustomOpportunityResolver *opportunityResolver = [[CustomOpportunityResolver alloc] init]; 
   
   //Set custom opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory]  
              registerOpportunityResolver:[opportunityResolver autorelease]];
   ```

När spelaren läser in innehållet och den är av typen VOD eller LIVE händer något av följande: >
* Om innehållet är VOD används den anpassade innehållslösaren för att hämta annonstidslinjen för hela videon.
* Om innehållet är LIVE anropas den anpassade innehållslösaren varje gång en placeringsmöjlighet (referenspunkt) upptäcks i innehållet.
