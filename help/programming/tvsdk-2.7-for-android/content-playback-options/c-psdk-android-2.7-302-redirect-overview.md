---
description: 302 omdirigeringsoptimering minimerar antalet 302 omdirigeringssvar, vilket gör att programmet kan belastningsutjämna mer effektivt.
title: Omdirigeringsoptimering för HTTP 302
exl-id: fdbdc2b4-6c1a-4ab1-80e2-b5e079ffa906
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# Omdirigeringsoptimering för HTTP 302 {#http-redirect-optimization}

302 omdirigeringsoptimering minimerar antalet 302 omdirigeringssvar, vilket gör att programmet kan belastningsutjämna mer effektivt.

Om en huvudmanifestbegäran omdirigeras och 302-optimering aktiveras i spelaren kommer efterföljande begäranden för resurser från det manifestet att använda den slutliga domänplatsen, vilket förhindrar ytterligare 302 svar. Den här funktionen är aktiverad som standard och du kan ändra den här inställningen.

## Inaktivera eller aktivera 302 omdirigeringsoptimering {#section_8977448B268E41D69A8F75B60EB9DA3B}

Använd `useRedirectedUrl` egenskap som aktiverar 302 omdirigering ( `true`) eller av ( `false`).

<!--<a id="example_888749F70C8A43279D06A29BD68E7E4D"></a>-->

Till exempel:

```java
// Set useRedirectedUrl property to false 
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.setUseRedirectedUrl(false); 
 
//Set NetworkConfiguration on MediaPlayerItemConfig 
MediaPlayerItemConfig config = new MediaPlayerItemConfig (); 
config.setNetworkConfiguration(networkConfiguration); 
 
//Use this config when loading the MediaPlayerItem or calling replaceCurrentResource
```
