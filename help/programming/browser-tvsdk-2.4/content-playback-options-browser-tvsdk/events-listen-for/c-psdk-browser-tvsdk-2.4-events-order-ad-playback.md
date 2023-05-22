---
description: När din uppspelning inkluderar annonsering skickar webbläsarens TVSDK händelser/meddelanden i de sekvenser som förväntas. Spelaren kan implementera åtgärder baserat på händelser i den förväntade sekvensen.
title: Ordning på annonsevenemang
exl-id: fcc40aa8-9364-40a8-b2f2-9327e24819af
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Ordning på annonsevenemang{#order-of-advertising-events}

När din uppspelning inkluderar annonsering skickar webbläsarens TVSDK händelser/meddelanden i de sekvenser som förväntas. Spelaren kan implementera åtgärder baserat på händelser i den förväntade sekvensen.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

När annonser spelas upp är händelseordningen:

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* Följande skickas för varje annons i annonsbrytningen:

   * `AdobePSDK.PSDKEventType.AD_STARTED`
   * `AdobePSDK.PSDKEventType.AD_PROGRESS` (flera gånger under en annons uppspelning)
   * `AdobePSDK.PSDKEventType.AD_COMPLETED`

* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`

I följande exempel visas ett typiskt förlopp för annonsuppspelningshändelser:

```js
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_STARTED, onAdbreakStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_PROGRESS, onAdProgress); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED, onAdbreakCompleted);
```
