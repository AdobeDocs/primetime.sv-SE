---
title: Versionsinformation om Primetime
seo-title: Versionsinformation för Adobe Primetime
description: 'null'
seo-description: 'null'
translation-type: tm+mt
source-git-commit: a42c5b4478967822c920d96b05d5f04a6dec8c25
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# Versionsinformation om Primetime

Välkommen till versionsinformationen för Adobe Primetime. Dokumenten som visas i den vänstra navigeringen innehåller versionsspecifik information, systemkrav, begränsningar, åtgärdade problem och kända fel.

## Förbättringar och korrigeringar i PTAI 21.2.2

Versionen innehåller stöd för infogning/synkronisering av EXT-X-IMAGE-STREAM-INF-strömmar i HLS-strömmar. Funktionen aktiveras via en konfiguration på serversidan. Kontakta din tekniska kontorepresentant för att aktivera funktionen.

## Korrigeringar i TVSDK 3.13 Android

Den här versionen innehåller en lösning på problemet med frysning av DRM-strömmen på Widewin eller visning av svarta bildrutor på ABR-omkopplare på FireTV-enheter, som innehåller 3:e generationens Fire TV-enheter av typen Pendant och Fire TV Cube 1:a och 2:a generationen.

Du löser problemet genom att ange API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)` för de angivna Fire TV-enheterna innan du påbörjar uppspelningen. Standardvärdet är false.

Mer information finns i [versionsinformationen för TVSDK for Android](../release-notes/tvsdk-3x-android.md).

## Förbättringar och korrigeringar i versionsinformation för TVSDK 3.12 iOS

Versionen fokuserade på att lösa de vanligaste kundproblemen.

Mer information om den aktuella versionen för [iOS](../release-notes/tvsdk-3x-ios.md) finns här.

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
