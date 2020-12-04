---
description: Om programmet behöver hantera händelser som skickas från funktionshanteraren måste det registrera hanteraren i filen PlayerFragment.java.
seo-description: Om programmet behöver hantera händelser som skickas från funktionshanteraren måste det registrera hanteraren i filen PlayerFragment.java.
seo-title: Hantera händelser
title: Hantera händelser
uuid: 13639f02-0dcc-4a0a-8524-515da5478006
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 2%

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
