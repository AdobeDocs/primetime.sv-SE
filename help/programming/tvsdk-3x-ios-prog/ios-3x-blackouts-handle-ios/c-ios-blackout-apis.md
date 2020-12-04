---
description: TVSDK innehåller API-element som är användbara när du implementerar utfall, inklusive metoder, metadata och meddelanden.
seo-description: TVSDK innehåller API-element som är användbara när du implementerar utfall, inklusive metoder, metadata och meddelanden.
seo-title: API-element för svart
title: API-element för svart
uuid: f87f4ed0-3f97-48bd-bceb-28357a978964
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# API-element för svart {#blackout-api-elements}

TVSDK innehåller API-element som är användbara när du implementerar utfall, inklusive metoder, metadata och meddelanden.

Du kan använda följande när du implementerar en svartpunkt i din spelare.

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Sparar den inlästa resursen som bakgrundsresurs. Om `replaceCurrentItemWithPlayerItem` anropas efter den här metoden fortsätter TVSDK att hämta bakgrundsobjektets manifest tills du anropar `unregisterCurrentBackgroundItem`, `stop` eller `reset`.

   * `unregisterCurrentBackgroundItem` Anger att bakgrundsobjektet är noll och stoppar hämtning och tolkning av bakgrundsmanifestet.

* **PTMetadata.** PTBlackoutMetadataEn  `PTMetadata` klass som är specifik för strömavbrott.

   På så sätt kan du ange intervall som inte kan sökas (en matris på `CMTimeRanges`) på TVSDK. TVSDK söker efter dessa intervall varje gång användaren söker. Om den är inställd och användaren söker i ett intervall som inte kan sökas tvingar TVSDK användaren till slutet av det intervall som inte går att söka i.

* **START HERE** **** NEXTPTAdMetadataAktivera eller inaktivera förregistrering i en liveström genom  `enableLivePreroll` att ange YES eller NO. Om NEJ, gör inte TVSDK något explicit annonsserveranrop för pre-roll-annonser före innehållsuppspelningen och spelar därför inte upp pre-roll. Detta påverkar inte mittrullarna. Standardvärdet är JA.

* **NSNNotifications**

   * `PTTimedMetadataChangedInBackgroundNotification` - Anges när TVSDK identifierar en prenumerationstagg i bakgrundsmanifestet och en ny  `PTTimedMetadata` instans förbereds utifrån den. Meddelandets objekt är den `PTMediaPlayerItem`-instans som spelas upp just nu. Du kan hämta `PTTimedMetadata`-instansen från meddelandets `userInfo`-ordlista med `PTTimedMetadataKey`-tangenten.

   * `PTBackgroundManifestErrorNotification` - Anges när mediespelaren helt inte kan läsa in bakgrundsmanifestet, det vill säga att alla strömmens URL returnerar antingen ett fel eller ett ogiltigt svar. Meddelandets objekt är den `PTMediaPlayerItem`-instans som spelas upp just nu.

* **PTNotification**

   * `BACKGROUND_MANIFEST_WARNING`

      * Kod: 204000
      * Typ: Varning
      * Fel vid hämtning av bakgrundsmanifest.
   * `INVALID_SEEK_WARNING` Skickas när ett sökförsök görs i ett icke sökbart område (i  `nonSeekableRanges` uppsättningen  `PTBlackoutMetadata`).