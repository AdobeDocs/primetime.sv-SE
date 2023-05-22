---
description: 302 omdirigeringsoptimering minimerar antalet 302 omdirigeringssvar, vilket gör att programmet kan belastningsutjämna mer effektivt.
title: Inaktivera eller aktivera 302 omdirigeringsoptimering
exl-id: b1bdb6d6-b34d-4e0a-8c96-7fd4ce77b5c9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# Omdirigeringsoptimering för HTTP 302 {#http-302-redirect-optimization}

302 omdirigeringsoptimering minimerar antalet 302 omdirigeringssvar, vilket gör att programmet kan belastningsutjämna mer effektivt.

Om en huvudmanifestbegäran omdirigeras och 302-optimering aktiveras i spelaren kommer efterföljande begäranden för resurser från det manifestet att använda den slutliga domänplatsen, vilket förhindrar ytterligare 302 svar.

Den här funktionen är aktiverad som standard och du kan ändra den här inställningen.

## Inaktivera eller aktivera 302 omdirigeringsoptimering{#disable-or-enable-redirect-optimization}

Använd `useRedirectedUrl` egenskapen för att aktivera 302 omdirigering (true) eller av (false).
Till exempel:

```java
// Set useRedirectedUrl property to false 
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.setUseRedirectedUrl(false); 
 
//Set NetworkConfiguration as Metadata: 
MetadataNode resourceMetadata = new MetadataNode();  
resourceMetadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(),  
                         networkConfiguration); 
 
//Call MediaResource.createFromURL to set the metadata: 
MediaResource resource = MediaResource.createFromURL(url, resourceMetadata); 
  
//Load the resource 
mediaPlayer.replaceCurrentItem(resource);
```
