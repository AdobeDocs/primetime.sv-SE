---
description: Om programmet behöver hantera händelser som skickas från funktionshanteraren måste det registrera hanteraren i filen PlayerFragment.java.
title: Hantera händelser
exl-id: 4c9a76bb-071e-4408-819c-a7611fe615cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# Hantera händelser {#handling-events}

Om programmet behöver hantera händelser som skickas från funktionshanteraren måste det registrera hanteraren i filen PlayerFragment.java.

Till exempel:

```
private final AdsManager.AdsManagerEventListener adsManagerEventListener =  
  new AdsManager.AdsManagerEventListener() { 
 
    // add the ads functionality... 
 
} 
 
//Register the listener 
adsManager.addEventListener(adsManagerEventListener);
```
