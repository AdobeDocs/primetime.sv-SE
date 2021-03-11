---
description: Du kan ställa in en gränssnittskontroll för att justera volymen för videon.
title: Ange volymkontroll
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 2%

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