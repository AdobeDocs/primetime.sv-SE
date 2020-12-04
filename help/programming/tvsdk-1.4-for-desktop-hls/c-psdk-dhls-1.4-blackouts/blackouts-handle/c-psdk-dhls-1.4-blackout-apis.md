---
description: TVSDK innehåller API-element som är användbara när du implementerar utfall, inklusive metoder, metadata och meddelanden.
seo-description: TVSDK innehåller API-element som är användbara när du implementerar utfall, inklusive metoder, metadata och meddelanden.
seo-title: API-element för svart
title: API-element för svart
uuid: 65e1668c-6a19-4910-83a2-46d364e94e5f
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# API-element för svart{#blackout-api-elements}

TVSDK innehåller API-element som är användbara när du implementerar utfall, inklusive metoder, metadata och meddelanden.

Du kan använda följande när du implementerar en svartpunkt i din spelare.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Sparar den inlästa resursen som bakgrundsresurs. Om `replaceCurrentResource` anropas efter den här metoden fortsätter TVSDK att hämta bakgrundsobjektets manifest tills du anropar `unregisterCurrentBackgroundItem`.

   * `unregisterCurrentBackgroundItem`  Rensar den angivna bakgrundsresursen och avbryter hämtning och tolkning av bakgrundsmanifestet.

* **** BlackoutMetadataEn metadatatyp som är specifik för strömavbrott.

   På så sätt kan du ange intervall som inte kan sökas (ett ytterligare `TimeRange`-attribut med namnet `nonseekableRange`) på TVSDK. TVSDK söker efter dessa intervall (om den önskade sökpositionen ligger inom `nonseekableRange`) varje gång användaren söker. Om den är inställd och användaren söker i ett intervall som inte kan sökas tvingar TVSDK användaren till sluttiden för `seekableRange`.

* **START HERE** **** NEXTDefaultMetadataKeysAktivera eller inaktivera förhandsgranskning i en liveström genom  `ENABLE_LIVE_PREROLL` att ange värdet true eller false. Om värdet är false gör inte TVSDK något explicit annonsserveranrop för pre-roll-annonser före innehållsuppspelningen och spelar därför inte upp pre-roll. Detta påverkar inte mittrullarna. Standardvärdet är true.

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` händelsetyp - Skickas när TVSDK identifierar en prenumerationstagg i bakgrundsmanifestet.

* **Meddelanden**

   * `BACKGROUND_MANIFEST_WARNING`

      * Kod: 204000
      * Typ: Varning
      * Fel vid hämtning av bakgrundsmanifest.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` Skickas när ett sökförsök görs i ett område som inte kan sökas.


