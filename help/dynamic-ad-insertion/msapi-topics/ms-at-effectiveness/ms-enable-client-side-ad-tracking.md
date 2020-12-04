---
description: Du kan aktivera annonsspårning på klientsidan genom att lägga till parametrarna paketeringsläge och paketeringsversion i Bootstrap URL-begäran.
seo-description: Du kan aktivera annonsspårning på klientsidan genom att lägga till parametrarna paketeringsläge och paketeringsversion i Bootstrap URL-begäran.
seo-title: Aktivera annonsspårning på klientsidan
title: Aktivera annonsspårning på klientsidan
uuid: 0a825756-1d9a-43c5-bc22-9b366f39fdbb
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 1%

---


# Aktivera annonsspårning på klientsidan {#enable-client-side-ad-tracking}

Du kan aktivera annonsspårning på klientsidan genom att lägga till parametrarna `pttrackingmode` och `pttrackingversion` i Bootstrap URL-begäran.

När annonsspårning är aktiverat på klientsidan kan du även hämta annonsspårningsmetadata med API-URL:en för spårning. Mer information finns i [Frågeparametrar](../../msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md).

Om du vill spåra annonser på klientsidan använder du API-URL:en för spårning.

1. Lägg till följande frågeparametrar i URL:en för manifestserverbegäran:

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

Exempel:

```
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
