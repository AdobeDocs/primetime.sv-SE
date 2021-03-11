---
title: Inaktivera annonser före rullning
description: Inaktivera annonser före rullning
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 0%

---


# Inaktivera förrollsannonser{#disable-pre-roll-ads}

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

