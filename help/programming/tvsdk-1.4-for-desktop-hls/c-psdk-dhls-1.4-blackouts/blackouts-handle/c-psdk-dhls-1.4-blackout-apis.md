---
description: TVSDK innehåller API-element som är användbara när du implementerar utfall, inklusive metoder, metadata och meddelanden.
title: API-element för svart
exl-id: 9dae236b-0bd8-4fce-9163-628d4ed94f02
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# API-element för svart{#blackout-api-elements}

TVSDK innehåller API-element som är användbara när du implementerar utfall, inklusive metoder, metadata och meddelanden.

Du kan använda följande när du implementerar en svartpunkt i din spelare.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Sparar den inlästa resursen som bakgrundsresurs. If `replaceCurrentResource` anropas efter den här metoden fortsätter TVSDK att hämta bakgrundsobjektets manifest tills du anropar `unregisterCurrentBackgroundItem`.

   * `unregisterCurrentBackgroundItem`  Rensar den angivna bakgrundsresursen och avbryter hämtning och tolkning av bakgrundsmanifestet.

* **BlackoutMetadata** En metadatatyp som är specifik för strömavbrott.

   Detta gör att du kan ange intervall som inte kan sökas (ytterligare `TimeRange` attribut anropat `nonseekableRange`) på TVSDK. TVSDK söker efter dessa intervall (om den önskade sökpositionen ligger inom en `nonseekableRange`) varje gång användaren söker. Om den är inställd och användaren söker i ett intervall som inte kan sökas tvingar TVSDK användaren till sluttiden för `seekableRange`.

* **STARTA HÄR NÄSTA** **DefaultMetadataKeys** Aktivera eller inaktivera inledning i en liveström genom att ange `ENABLE_LIVE_PREROLL` till true eller false. Om värdet är false gör inte TVSDK något explicit annonsserveranrop för pre-roll-annonser före innehållsuppspelningen och spelar därför inte upp pre-roll. Detta påverkar inte mittrullarna. Standardvärdet är true.

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` händelsetyp - Skickas när TVSDK identifierar en prenumerationstagg i bakgrundsmanifestet.

* **Meddelanden**

   * `BACKGROUND_MANIFEST_WARNING`

      * Kod: 204000
      * Typ: Varning
      * Fel vid hämtning av bakgrundsmanifest.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` Skickas när ett sökförsök görs i ett område som inte kan sökas.
