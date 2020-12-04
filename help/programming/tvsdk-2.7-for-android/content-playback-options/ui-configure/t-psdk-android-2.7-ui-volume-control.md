---
description: Du kan ställa in en gränssnittskontroll för att justera volymen för videon.
seo-description: Du kan ställa in en gränssnittskontroll för att justera volymen för videon.
seo-title: Ange volymkontroll
title: Ange volymkontroll
uuid: f1e959e0-1817-4ccb-8adc-3eba09c91887
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 1%

---


# Ange volymkontroll {#provide-volume-control}

Du kan ställa in en gränssnittskontroll för att justera volymen för videon.

1. Kontrollera att spelaren har en giltig status för det här kommandot i återanropsfunktionen för volymkontrollens gränssnittselement.

   >[!TIP]
   >
   >Alla statusvärden, förutom FRISLÄPPT, är giltiga.

1. Ring `setVolume` för att ställa in ljudvolymen.

   Exempel:

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   Värdet för volymen representerar den begärda volymen uttryckt som en del av den maximala volymen, där `0` är tyst och `1` är den maximala volymen.

