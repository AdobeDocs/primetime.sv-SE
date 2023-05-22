---
description: Funktionshanterarna fungerar som wrappers runt TVSDK-biblioteket.
title: Referensimplementationsstruktur
exl-id: cf102ccc-2e31-4197-a321-e485f77ba754
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# Referensimplementationsstruktur {#reference-implementation-structure}

Funktionshanterarna fungerar som wrappers runt TVSDK-biblioteket.

I Java är klasser strukturerade i en hierarki. Till exempel all gränssnittsrelaterad kod under `com.adobe.primetime.reference.ui` och alla funktionshanterare är under `com.adobe.primetime.reference.manager`.

Referensimplementeringen för Primetime innehåller följande paket:

| Paket | Beskrivning |
|--- |--- |
| [com.adobe.primetime.reference](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/PrimetimeReference.html) | Den här klassen utökar android.app.Application. |
| [com.adobe.primetime.reference.advertising](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/advertising/package-summary.html) | Innehåller kod för anpassade annonser. |
| [com.adobe.primetime.reference.config](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html) | Innehåller den gränssnittskod som krävs för att konfigurera funktionshanterarna. |
| [com.adobe.primetime.reference.drm](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/drm/package-summary.html) | Innehåller hjälpklasser för DRM. |
| [com.adobe.primetime.reference.feeds](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/feeds/package-summary.html) | Adaptrarna och objektadaptrarna för gränssnitt, plattform och referensinformation. Innehåller även koden FeedAdapterFactory, ContentRenditionInfo och XMLParserHelper. |
| [com.adobe.primetime.reference.log](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/logging/package-summary.html) | Innehåller klasser för lokal och fjärransluten loggning. |
| [com.adobe.primetime.reference.manager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/package-summary.html) | Här hittar du både funktionshanterare och ManagerFactory. Det finns två funktionshanterare för valfria funktioner som du kan aktivera eller inaktivera: <ul><li>En funktionshanterare som är namnet på funktionen, till exempel CCManager. Den här funktionshanteraren är inaktiverad och tillhandahåller standardbeteendet för inaktiverat.</li><li>En funktionshanterare som har On som tillägg till funktionshanterarens namn, till exempel CCManagerOn. Den här funktionshanteraren innehåller exempelkod för den aktiverade funktionen.</li></ul> |
| [com.adobe.primetime.reference.ui.catalog](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/catalog/package-summary.html) | Innehåller gränssnittskod för katalogen. |
| [com.adobe.primetime.reference.ui.log](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/log/package-summary.html) | Innehåller gränssnittskod för loggen. |
| [com.adobe.primetime.reference.ui.player](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/package-summary.html) | Innehåller gränssnittskod för spelaren. |
| [com.adobe.primetime.reference.ui.settings](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/settings/package-summary.html) | Innehåller gränssnittskod för inställningar. |
| [com.adobe.primetime.reference.utils](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/package-summary.html) | Innehåller allmänna verktygsklasser. |
| [com.adobe.primetime.reference.utils.http](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/http/package-summary.html) | Innehåller `HTTP-specific` verktygsklasser. |
