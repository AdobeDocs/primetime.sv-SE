---
description: 302 omdirigeringsoptimering minimerar antalet 302 omdirigeringssvar, vilket gör att programmet kan belastningsutjämna mer effektivt.
seo-description: 302 omdirigeringsoptimering minimerar antalet 302 omdirigeringssvar, vilket gör att programmet kan belastningsutjämna mer effektivt.
seo-title: Omdirigeringsoptimering för HTTP 302
title: Omdirigeringsoptimering för HTTP 302
uuid: d3009c6c-320a-4c0f-b6ba-bf6473049823
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---


# Omdirigeringsoptimering för HTTP 302 {#http-redirect-optimization}

302 omdirigeringsoptimering minimerar antalet 302 omdirigeringssvar, vilket gör att programmet kan belastningsutjämna mer effektivt.

Om en huvudmanifestbegäran omdirigeras och 302-optimering aktiveras i spelaren kommer efterföljande begäranden för resurser från det manifestet att använda den slutliga domänplatsen, vilket förhindrar ytterligare 302 svar. Den här funktionen är aktiverad som standard och du kan ändra den här inställningen.

>[!IMPORTANT]
>
>Den här funktionen stöds bara i de certifierade webbläsare som stöder egenskapen `responseURL` i `XMLHttpRequest`-objektet.

Kom ihåg följande information för Flash fallback:

* Slutanvändarna måste ha Adobe Flash Player version 23 eller senare installerat.
* Om dataströmmens integritet är inaktiverad stöds 302-omdirigering endast i certifierade webbläsare.

## Inaktiverar 302 omdirigeringsoptimering {#disabling-redirect-optimization}

Du kan använda egenskapen useRedirectedUrl för att aktivera 302-omdirigering (true) eller inaktivering (false).

Exempel:

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
