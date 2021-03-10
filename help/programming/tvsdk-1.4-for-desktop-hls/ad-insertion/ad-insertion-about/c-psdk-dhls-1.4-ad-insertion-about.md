---
description: Annonsinfogningen åtgärdar annonser för video-on-demand (VOD), för liveströmning och för linjär direktuppspelning med annonsspårning och annonsuppspelning. TVSDK skickar de begärda förfrågningarna till annonsservern, tar emot information om annonser för det angivna innehållet och placerar annonserna i innehållet i faser.
title: Infoga annonser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---


# Översikt {#inserting-ads-overview}

Annonsinfogningen åtgärdar annonser för video-on-demand (VOD), för liveströmning och för linjär direktuppspelning med annonsspårning och annonsuppspelning. TVSDK skickar de begärda förfrågningarna till annonsservern, tar emot information om annonser för det angivna innehållet och placerar annonserna i innehållet i faser.

En *`ad break`* innehåller en eller flera annonser som spelas upp i sekvens. TVSDK infogar annonser i huvudinnehållet som medlemmar i en eller flera annonsbrytningar.

## Inaktivera förrollsannonser {#disable-preroll-ads}

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
