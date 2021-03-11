---
description: Annonsupplösning och annonsinläsning kan orsaka en oacceptabel fördröjning för en användare som väntar på att uppspelningen ska starta. Funktionen Lazy Ad Loading Resolving kan minska startfördröjningen. Annonserna kan nu lösas vid ett angivet intervall innan annonsbrytningens position. Detta uppnås genom att använda en strategi med två spelare.
title: Just-in-Time-annonsvisning
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---


# Just-in-Time-annons som löser {#just-in-time-ad-resolving}

Annonsupplösning och annonsinläsning kan orsaka en oacceptabel fördröjning för en användare som väntar på att uppspelningen ska starta. Funktionen Lazy Ad Loading Resolving kan minska startfördröjningen. Annonserna kan nu lösas vid ett angivet intervall innan annonsbrytningens position. Detta uppnås genom att använda en strategi med två spelare.

**Grundläggande annonslösning och inläsningsprocess:**

1. TVSDK hämtar ett manifest (playlist) och *löser* alla annonser.
1. TVSDK *läser in* alla annonser och sätter ihop annonssegmenten i manifesten.
1. TVSDK flyttar spelaren till PREPARED-status och uppspelningen av innehåll börjar.

Spelaren använder URL:erna i manifestet för att hämta annonsinnehållet (kreatörerna), ser till att annonsinnehållet är i ett format som TVSDK kan spela upp, och TVSDK placerar annonserna på tidslinjen. Denna grundläggande process för att lösa och läsa in annonser kan orsaka en orimligt lång fördröjning för en användare som väntar på att spela upp sitt innehåll, särskilt om manifestet innehåller flera annons-URL:er.

**Lazy Ad Resolving:**

1. TVSDK hämtar spellistan.
1. TVSDK *löser och läser in* alla pre-roll-annonser, flyttar spelaren till PREPARED-status och innehållsuppspelningen börjar.
1. TVSDK *löser* varje annonsbrytning före sin position baserat på det värde som definieras i `PTAdMetadata::delayAdLoadingTolerance`.

Som standard är till exempel `delayAdLoadingTolerance` inställt på 5 sekunder. Om en AdBreak är inställd på att spelas upp kl. 3:00 löses den kl. 2:55:00. Du kanske vill öka värdet om du tror att annonsupplösningen tar längre tid än 5 sekunder.

>[!IMPORTANT]
>
>**Faktorer att tänka på när det gäller Lazy Ad Resolving:**
>* Lazy Ad Resolving stöds bara för VOD-strömmar med positionerna SERVER_MAP och signaleringsläge.
>* Lazy Ad Resolving är inte aktiverat som standard. Du måste ange `PTAdMetadata::delayAdLoading` = JA för att aktivera den.
>* Lazy Ad Resolving är inte kompatibelt med funktionen Instant On. Mer information om Direkt på finns i [Direkt på](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md).
>* Bild-i-bild-läget stöds inte med Lazy Ad Resolving. Inaktivera alla bild-i-bild-lägen om du aktiverar Lazy Ad Resolving.
>* Lazy-annonsupplösningen påverkar inte pre-roll-annonser.

>


**Aktivera lat och löst**

Du kan aktivera eller inaktivera funktionen Lazy Ad Resolving med den befintliga Lazy Ad Loading-mekanismen (Lazy Ad Resolving är inaktiverat som standard).

Du kan aktivera Lazy Ad Resolving genom att ställa in `PTAdMetadata::delayAdLoading`= YES när du ställer in dina annonsmetadata.

**API:er som är relevanta för lata annonsupplösningar:**

```
Class:    PTAdMetadata 
Properties: 
  
/** 
 * Property to define whether ad break resolution must be delayed until after stream start or not. 
 * When this value is NO, ads are resolved before stream start and spliced into the content when possible allowing  
   for a seamless playback experience. 
 * When this value is YES, ads are displayed in a secondary video player instance and resolved lazily only when  
   needed. 
 * Default value is NO 
 */ 
@property (nonatomic, assign) BOOL delayAdLoading; 
  
/** 
 * Property to define the lookahead for ad break resolution.  Ad breaks will be resolved when they occur between  
   the playhead time and the specified tolerance. 
 * If set to zero, the ad will be resolved immediately before playing the ad.  This may cause a slight delay in the  
   playback of the ads. 
 * Default value is 5.0 or 5 seconds. 
 */ 
  
@property (nonatomic, assign) NSTimeInterval delayAdLoadingTolerance;
```
