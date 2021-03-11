---
description: Dessa klasser innehåller information om annonser som förekommer i en tidslinje.
title: Tidslinjeannonsklasser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---


# Annonsklasser för tidslinje {#timeline-advertising-classes}

Dessa klasser innehåller information om annonser som förekommer i en tidslinje.

Paket: [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/package-detail.html)
Paket: [com.adobe.mediacore.timeline.advertising.policy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/package-detail.html)

| Namn | Beskrivning |
|---|---|
| [Annons](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | En klass som definierar Ad-förkortningen och som innehåller all annonsinformation. Den definieras av ett unikt ID, en varaktighet och ett `MediaResource`. `MediaResource` innehåller URL:en där det faktiska annonsinnehållet finns. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | En klass som representerar en resurs som ska visas. En klass som representerar en annonsresurs. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | En klass som ger en enhetlig vy på flera annonser som kommer att spelas upp någon gång under uppspelningen. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakPolicy.html) | En uppräkning som definierar annonsuppspelningsprincipen som relaterar till användaren som åsidosätter annonser vid sökning. |
| [AdBreakTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreakTimelineItem.html) | Tidslinjeobjekt som är associerat med en viss annonsbrytning. |
| [AdBreakWatchedPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakWatchedPolicy.html) | Uppräkningsklass för möjliga principer för när en annonsbrytning ska markeras som bevakad. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | En klass som representerar en klickinstans som är associerad med en resurs. Den här instansen innehåller information om klicknings-URL:en och rubriken som kan användas för att ge användaren mer information. |
| [AdPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicy.html) | Uppräkningsklass för möjliga principer för var en annonsbrytning ska återupptas efter sökning eller uppspelning med trick. |
| [AdPolicyMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicyMode.html) | Uppräkningsklass som visar hur spelaren spelas upp, t.ex. sökning eller normal uppspelning. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Gränssnitt som definierar egenskaper för `AdPolicySelector` API-anrop. Dessa egenskaper utgör kontexten för att framtvinga varje annonsbeteende. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Ett gränssnitt för annonsprincipväljare för att framtvinga annonsbeteenden. Program kan anpassa sig till det här gränssnittet genom att implementera alla nödvändiga metoder eller genom att utöka den befintliga standardprincipväljarklassen för att anpassa specifika beteenden. |
| [AdTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdTimelineItem.html) | Tidslinjeobjekt som är associerat med en viss annons. |
| [AuditudeAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AuditudeAdResolver.html) | En klass som hanterar primetime och löser problem i TVSDK-processen. |
| [AdType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdType.html) | Uppräkning av alla annonstyper som stöds av TVSDK. |
| [MetadataAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/MetadataAdResolver.html) | Klass. |

