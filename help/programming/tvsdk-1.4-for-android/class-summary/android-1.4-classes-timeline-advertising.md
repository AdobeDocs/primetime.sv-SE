---
description: Dessa klasser innehåller information om annonser som förekommer i en tidslinje.
seo-description: Dessa klasser innehåller information om annonser som förekommer i en tidslinje.
seo-title: Tidslinjeannonsklasser
title: Tidslinjeannonsklasser
uuid: 4e6ca9fb-9e68-4625-a24b-386a50333862
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Tidslinjeannonsklasser{#timeline-advertising-classes}

Dessa klasser innehåller information om annonser som förekommer i en tidslinje.

Paket: [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/package-summary.html)

Paket: [com.adobe.mediacore.timeline.advertising.audiude](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/package-summary.html)

| Namn | Beskrivning |
|--- |--- |
| [Annons](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | En klass som definierar Ad-förkortningen och som innehåller all annonsinformation. Den definieras av ett unikt ID, en varaktighet och en `MediaResource`. Innehåller den URL-adress där det faktiska annonsinnehållet finns. `MediaResource` |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | En klass som representerar en resurs som ska visas. En klass som representerar en annonsresurs. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | En klass som ger en enhetlig vy på flera annonser som kommer att spelas upp någon gång under uppspelningen. |
| [AdBreakPlacement](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPlacement.html) | Åtgärdsklass för annonsradbrytning. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPolicy.html) | En uppräkning som definierar annonsuppspelningsprincipen som relaterar till användaren som åsidosätter annonser vid sökning. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | En klass som representerar en klickinstans som är associerad med en resurs. Den här instansen innehåller information om klicknings-URL:en och rubriken som kan användas för att ge användaren mer information. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicyInfo.html) | Gränssnitt som definierar egenskaper för API-anrop till AdPolicySelector. Dessa egenskaper utgör kontexten för att framtvinga varje annonsbeteende. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicySelector.html) | Ett gränssnitt för annonsprincipväljare för att framtvinga annonsbeteenden. Program kan anpassa sig till det här gränssnittet genom att implementera alla nödvändiga metoder eller genom att utöka den befintliga standardprincipväljarklassen för att anpassa specifika beteenden. |
| `auditude.AuditudeAdProvider` | Föråldrat. Använd AuditudeResolver. |
| [AuditudeResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeResolver.html) | En klass som hanterar primetime och löser i frasprocessen. |
| [AuditudeTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeTracker.html) | En klass som implementerar ContentTracker-gränssnittet och definierar Primetime-annonspårningshändelser. |
| [ContentResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentResolver.html) | En klass som hanterar annonsupplösningsdelen i frasprocessen. |
| [ContentTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentTracker.html) | Gränssnitt som definierar det protokoll som du måste implementera om du vill skapa en annonsspårningsmodul som är utformad för att integreras med biblioteket eller en anpassad annonsspårare. Det här gränssnittet kräver att du definierar hur annonseringshändelser rapporteras till det fjärranslutna annonsspårningssystemet. |
| [PlacementInformation](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/PlacementInformation.html) | En klass som abstraherar en begäran om placeringsinformation. Varje löst annons måste ha en placeringsinformation kopplad till sig. Placeringsinformationen beskriver var annonsen är avsedd att placeras på tidslinjen. Den innehåller information om: <ul><li>Placeringsposition (i ms) </li><li>Placeringens typ (före-, mitt- eller efterrullning) </li><li>Längden på det huvudinnehållssegment som ska ersättas</li></ul> |
