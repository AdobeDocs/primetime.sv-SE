---
description: Om programmet behöver hantera händelser som skickas från funktionshanteraren måste det registrera hanteraren i filen PlayerFragment.java.
title: Hantera händelser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
