---
description: 302 omdirigeringsoptimering minimerar antalet 302 omdirigeringssvar, vilket gör att programmet kan belastningsutjämna mer effektivt.
seo-description: 302 omdirigeringsoptimering minimerar antalet 302 omdirigeringssvar, vilket gör att programmet kan belastningsutjämna mer effektivt.
seo-title: Omdirigeringsoptimering för HTTP 302
title: Omdirigeringsoptimering för HTTP 302
uuid: 58593d5f-a639-4d87-9589-dba6b2dbba38
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# HTTP 302 - omdirigeringsoptimering{#http-redirect-optimization}

302 omdirigeringsoptimering minimerar antalet 302 omdirigeringssvar, vilket gör att programmet kan belastningsutjämna mer effektivt.

Om en huvudmanifestbegäran omdirigeras och 302-optimering aktiveras i spelaren kommer efterföljande begäranden för resurser från det manifestet att använda den slutliga domänplatsen, vilket förhindrar ytterligare 302 svar.

Den här funktionen är inaktiverad som standard och du kan ändra den här inställningen.

Om du aktiverar den här funktionen fungerar den bara korrekt om *alla* av följande villkor är uppfyllda: i annat fall sker ingen omdirigeringsoptimering och 302 svar fortsätter att inträffa:

* Ditt program kompilerades för Adobe 11.8 med `-swf-version` 21 eller senare.
* Dina slutanvändare har Adobe Flash Player 11.8 eller senare installerat.

>[!IMPORTANT]
>
>Inaktivera omdirigering av 302 för att säkerställa att cookies skickas med annonsförfrågningar. När 302-omdirigering är aktiverat kan annonsbegäran omdirigeras till en annan domän än den domän som cookien kom från.

## Inaktivera eller aktivera 302 omdirigeringsoptimering {#section_D6687FC44C61446F878008B629A5FA19}

Använd egenskapen `useRedirectedUrl` för att aktivera (true) eller inaktivera 302 omdirigering (false).

<!--<a id="example_B886777252B745AAB48B1FCC42C97A25"></a>-->

Exempel:

```
// Set useRedirectedUrl property to true 
var networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = true; 
  
//Set NetworkConfiguration as Metadata: 
var result:Metadata = new Metadata(); 
result.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                   networkConfiguration); 
  
var mediaResource = new MediaResource( url, MediaResourceType.HLS, result); 
  
// load the resource 
mediaPlayer.replaceCurrentResource( mediaResource, mediaPlayerItemConfig );
```

