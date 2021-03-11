---
description: Ni kan infoga annonser i ert VOD-innehåll och direktsänt/linjärt innehåll med hjälp av Adobe Primetime annonsbeslutsgränssnitt.
title: Krav för annonsering
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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

Följ därefter avsnittet: [Primetime och servermetadata](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).

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

Följ därefter avsnittet: [Primetime och servermetadata](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).
