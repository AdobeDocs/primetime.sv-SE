---
title: Inaktivera annonser före rullning
description: Inaktivera annonser före rullning
copied-description: true
exl-id: ff52588e-540e-4072-bec0-e531c8cb6fe3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
