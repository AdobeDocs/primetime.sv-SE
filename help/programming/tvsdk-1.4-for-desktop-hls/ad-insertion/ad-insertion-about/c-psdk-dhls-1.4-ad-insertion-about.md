---
description: Annonsinfogningen åtgärdar annonser för video-on-demand (VOD), för liveströmning och för linjär direktuppspelning med annonsspårning och annonsuppspelning. TVSDK skickar de begärda förfrågningarna till annonsservern, tar emot information om annonser för det angivna innehållet och placerar annonserna i innehållet i faser.
seo-description: Annonsinfogningen åtgärdar annonser för video-on-demand (VOD), för liveströmning och för linjär direktuppspelning med annonsspårning och annonsuppspelning. TVSDK skickar de begärda förfrågningarna till annonsservern, tar emot information om annonser för det angivna innehållet och placerar annonserna i innehållet i faser.
seo-title: Infoga annonser
title: Infoga annonser
uuid: 25c79822-a861-427b-b6a8-24714b21aae4
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Översikt {#inserting-ads-overview}

Annonsinfogningen åtgärdar annonser för video-on-demand (VOD), för liveströmning och för linjär direktuppspelning med annonsspårning och annonsuppspelning. TVSDK skickar de begärda förfrågningarna till annonsservern, tar emot information om annonser för det angivna innehållet och placerar annonserna i innehållet i faser.

En *`ad break`* innehåller en eller flera annonser som spelas upp i sekvens. TVSDK infogar annonser i huvudinnehållet som medlemmar i en eller flera annonsbrytningar.

## Inaktivera annonser före rullning {#disable-preroll-ads}

Om du vill inaktivera pre-roll ändrar du standardgeneratorerna för affärsmöjlighet så att de inte gör ett pre-roll-anrop. Standardgeneratorerna för affärsmöjlighet är:

```
@inheritDoc 
*/ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
result.push(new AdSignalingModeOpportunityGenerator()); 
result.push(new SpliceOutOpportunityGenerator()); 
return result; 
}
```

Om du vill inaktivera förregistrering för liveströmmar ändrar du ovanstående så att endast SpliceOutOpportunityGenerator ingår:

```
@inheritDoc 
*/ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
if (preroll_enabled == true) { result.push(new AdSignalingModeOpportunityGenerator()); } 
 
result.push(new SpliceOutOpportunityGenerator()); 
return result; 
}
```
