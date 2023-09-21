---
description: Du kan ställa in en gränssnittskontroll för att justera volymen för videon.
title: Tillhandahåll volymkontroll
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Tillhandahåll volymkontroll {#provide-volume-control}

Du kan ställa in en gränssnittskontroll för att justera volymen för videon.

1. Kontrollera att spelaren har en giltig status för det här kommandot i återanropsfunktionen för volymkontrollens gränssnittselement.

   >[!TIP]
   >
   >Alla statusvärden, förutom FRISLÄPPT, är giltiga.

1. Utlysning `setVolume` för att ställa in ljudvolymen.

   Till exempel:

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   Värdet för volymen representerar den begärda volymen uttryckt som en andel av den maximala volymen, där `0` är tyst och `1` är den högsta volymen.
