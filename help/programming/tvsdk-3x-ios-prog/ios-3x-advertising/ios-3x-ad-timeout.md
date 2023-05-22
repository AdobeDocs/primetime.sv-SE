---
description: Ni kan infoga annonser i ert VOD-innehåll och direktsänt/linjärt innehåll med hjälp av Adobe Primetime annonsbeslutsgränssnitt.
title: Krav för annonsering
exl-id: b162e5b0-9f6c-46de-85de-97cec009a9b7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Timeout för annons {#ad-timeout}

## Krav för AV Foundation {#av-foundation-requirements}

När det gäller VOD-innehåll bör sammanfogningen av spellistor, som innefattar inläsning av huvudinnehållsmanifestet, upplösning och inläsning av annonsmanifestet, slutföras inom 35 sekunder.

När det gäller Live-innehåll ska matchningen av spellistan slutföras inom 20 sekunder varje gång spellistan uppdateras.

**API:er som är relevanta för AdResolution-timeout**

```
/** @name Properties */
/** The default timeout value (in seconds) for resolution of ad requests is 15 seconds.
*
*/
*
@property (notatomic, assign) double adResolutionTimeout;
```

Du kan ställa in adResolutionTimeout genom att ställa in PTAdMetadata::adResolutionTimeout när du ställer in annonsmetadata.

```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adResolutionTimeout = 15 seconds
```

Följ därefter avsnittet: [Metadata för Primetime och server](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).

**API:er som är relevanta för AdManifest-timeout**

```
/** @name Properties */
 /** The default timeout value (in seconds) for loading of ad manifests is 5 seconds.
 *
 */
 *
 @property (notatomic, assign) double adManifestTimeout; 
```

Du kan ange adManifestTimeout genom att ange PTAdMetadata::adManifestTimeout när du ställer in dina annonsmetadata.


```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adManifestTimeout = 5 seconds
```

Följ därefter avsnittet: [Metadata för Primetime och server](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).
