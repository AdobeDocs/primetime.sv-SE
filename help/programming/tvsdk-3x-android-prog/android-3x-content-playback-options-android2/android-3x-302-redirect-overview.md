---
description: 302 omdirigeringsoptimering minimerar antalet 302 omdirigeringssvar, vilket gör att programmet kan belastningsutjämna mer effektivt.
seo-description: 302 omdirigeringsoptimering minimerar antalet 302 omdirigeringssvar, vilket gör att programmet kan belastningsutjämna mer effektivt.
seo-title: Omdirigeringsoptimering för HTTP 302
title: Omdirigeringsoptimering för HTTP 302
uuid: 91ed8919-a3c1-4e57-9eaf-e3ba430de35f
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Omdirigeringsoptimering för HTTP 302 {#http-redirect-optimization}

302 omdirigeringsoptimering minimerar antalet 302 omdirigeringssvar, vilket gör att programmet kan belastningsutjämna mer effektivt.

Om en huvudmanifestbegäran omdirigeras och 302-optimering aktiveras i spelaren kommer efterföljande begäranden för resurser från det manifestet att använda den slutliga domänplatsen, vilket förhindrar ytterligare 302 svar. Den här funktionen är aktiverad som standard och du kan ändra den här inställningen.

## Inaktivera eller aktivera 302 omdirigeringsoptimering {#section_8977448B268E41D69A8F75B60EB9DA3B}

Använd egenskapen för att `useRedirectedUrl` aktivera ( `true`) eller inaktivera ( `false`) omdirigering till 302.

<!--<a id="example_888749F70C8A43279D06A29BD68E7E4D"></a>-->

Exempel:

```java
// Set useRedirectedUrl property to false 
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.setUseRedirectedUrl(false); 
 
//Set NetworkConfiguration on MediaPlayerItemConfig 
MediaPlayerItemConfig config = new MediaPlayerItemConfig (); 
config.setNetworkConfiguration(networkConfiguration); 
 
//Use this config when loading the MediaPlayerItem or calling replaceCurrentResource
```
