---
description: 302 omdirigeringsoptimering minimerar antalet 302 omdirigeringssvar, vilket gör att programmet kan belastningsutjämna mer effektivt.
title: Omdirigeringsoptimering för HTTP 302
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Omdirigeringsoptimering för HTTP 302 {#http-redirect-optimization}

302 omdirigeringsoptimering minimerar antalet 302 omdirigeringssvar, vilket gör att programmet kan belastningsutjämna mer effektivt.

Om en huvudmanifestbegäran omdirigeras och 302-optimering aktiveras i spelaren kommer efterföljande begäranden för resurser från det manifestet att använda den slutliga domänplatsen, vilket förhindrar ytterligare 302 svar. Den här funktionen är aktiverad som standard och du kan ändra den här inställningen.

>[!IMPORTANT]
>
>Den här funktionen stöds endast i certifierade webbläsare som stöder `responseURL` -egenskapen i `XMLHttpRequest` -objekt.

Kom ihåg följande information om reservlösningar för Flashar:

* Slutanvändarna måste ha Adobe Flash Player version 23 eller senare installerat.
* Om dataströmmens integritet är inaktiverad stöds 302-omdirigering endast i certifierade webbläsare.

## Inaktiverar 302 omdirigeringsoptimering {#disabling-redirect-optimization}

Du kan använda egenskapen useRedirectedUrl för att aktivera 302-omdirigering (true) eller inaktivering (false).

Till exempel:

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
