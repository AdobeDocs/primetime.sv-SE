---
description: Om programmet behöver hantera händelser som skickas från funktionshanteraren måste det registrera hanteraren i filen PlayerFragment.java.
title: Hantera händelser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 4%

---


# Hantera händelser {#handling-events}

Om programmet behöver hantera händelser som skickas från funktionshanteraren måste det registrera hanteraren i filen PlayerFragment.java.

Exempel:

```
private final AdsManager.AdsManagerEventListener adsManagerEventListener =  
  new AdsManager.AdsManagerEventListener() { 
 
    // add the ads functionality... 
 
} 
 
//Register the listener 
adsManager.addEventListener(adsManagerEventListener);
```
