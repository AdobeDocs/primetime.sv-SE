---
title: Versionsinformation om Primetime
description: Versionsinformation om Primetime
copied-description: true
exl-id: 29087a3e-f16e-4510-8d3a-ed2229700899
source-git-commit: fe0f5f3399d2e2ab3e07713fbcd29ede47888d98
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Versionsinformation om Primetime

Välkommen till versionsinformationen för Adobe Primetime. Dokumenten som visas i den vänstra navigeringen innehåller versionsspecifik information, systemkrav, begränsningar, åtgärdade problem och kända fel.

## Förbättringar och korrigeringar i PTAI 21.5.1

Versionen innehåller ny telemetri för kommande ändringar av instrumentpaneler och stöd för den inaktuella segmenteringstypen 0x01 (UPID) för SCTE-baserade cue-format.

Andra korrigeringar och detaljer finns i [Versionsinformation för Ad Insertion](/help/release-notes/ptai-21x-release-notes.md)

## Förbättringar och korrigeringar i TVSDK 3.13 iOS

I versionen finns stöd för DEMUXED HLS/CMAF-annonser (pre-roll, midroll och postroll) för LIVE-, VOD- och FER-strömmar.

Andra korrigeringar och detaljer finns i [TVSDK för iOS versionsinformation](../release-notes/tvsdk-3x-ios.md)

## Korrigeringar i TVSDK 3.13 Android

Den här versionen innehåller en lösning på problemet med frysning av DRM-strömmen på Widewin eller visning av svarta bildrutor på ABR-omkopplare på FireTV-enheter, som innehåller 3:e generationens Fire TV-enheter av typen Pendant och Fire TV Cube 1:a och 2:a generationen.

Du löser problemet genom att ange API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)` för de angivna Fire TV-enheterna innan du påbörjar uppspelningen. Standardvärdet är false.

Mer information finns i [versionsinformationen för TVSDK for Android](../release-notes/tvsdk-3x-android.md).

## Se även

| Användarhandbok | Beskrivning |
|--- |--- |
| [Hjälp om Primetime-programmering](/help/programming/home.md) | Lär dig utveckla program och videospelare med Java på Android-enheter och Objective-C på iOS-enheter. |
| [Hjälp om migrering och konvertering av Primetime](/help/migration-guides/home.md) | Beskriver konverterings- och migreringsprocessen för att gå över från din befintliga Primetime TVSDK Suite till nästa generations programsvit. |
| [Referensimplementering](/help/android-reference-implementation/home.md) | Hjälper dig att förstå TVSDK och ändra funktionshanterarna för att anpassa din personliga spelare. |
| [API-referenser för Primetime](/help/reference/api-references.md) | Innehåller detaljerad information om TVSDK-funktioner, datastrukturer och andra programmeringskonstruktioner. |
| [Digital Rights Management](/help/digital-rights-management/home.md) | Hjälper dig att lära dig mer om olika användarscenarier i Digital Rights Management (DRM) |
| [Hjälp om Primetime Ad Insertion](/help/primetime-ad-insertion/home.md) | Förklarar hur ni kan tjäna pengar på innehåll genom att infoga användarinriktade dynamiska annonser på servern och engagera målgruppen med personaliserade annonser. |
| [Arkiv](https://helpx.adobe.com/primetime/archives.html) | Ladda ned PDF:er av den arkiverade dokumentationen. |

## Användbara resurser

* [Lär känna Adobe Primetime](https://www.adobe.com/in/marketing/primetime.html)

* [Övervakning av samtidig användning](https://tve.helpdocsonline.com/concurrency-monitoring-introduction)

* [Primetime-autentisering](https://tve.helpdocsonline.com/home)

* [Adobe Primetime DRM-forum](https://forums.adobe.com/community/adobe_access)

* [Adobe Primetime Developer Resources](https://www.adobe.com/devnet/primetime.html)
