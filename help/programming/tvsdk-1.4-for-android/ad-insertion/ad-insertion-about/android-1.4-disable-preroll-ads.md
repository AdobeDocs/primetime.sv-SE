---
title: Inaktivera annonser före rullning
description: Inaktivera annonser före rullning
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 0%

---

# Inaktivera annonser före rullning{#disable-pre-roll-ads}

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
