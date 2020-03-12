---
description: Du kan ställa in en gränssnittskontroll för att justera volymen för videon.
seo-description: Du kan ställa in en gränssnittskontroll för att justera volymen för videon.
seo-title: Ange volymkontroll
title: Ange volymkontroll
uuid: c87fe656-0329-4c9c-b65b-43be48c77062
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

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