---
description: Du kan aktivera annonsspårning på klientsidan genom att lägga till parametrarna paketeringsläge och paketeringsversion i Bootstrap URL-begäran.
title: Aktivera annonsspårning på klientsidan
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 2%

---


# Aktivera annonsspårning på klientsidan {#enable-client-side-ad-tracking}

Du kan aktivera annonsspårning på klientsidan genom att lägga till parametrarna `pttrackingmode` och `pttrackingversion` i Bootstrap URL-begäran.

När annonsspårning är aktiverat på klientsidan kan du även hämta annonsspårningsmetadata med API-URL:en för spårning. Mer information finns i [Frågeparametrar](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md).

Om du vill spåra annonser på klientsidan använder du API-URL:en för spårning.

1. Lägg till följande frågeparametrar i URL:en för manifestserverbegäran:

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

Exempel:

```URL
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
