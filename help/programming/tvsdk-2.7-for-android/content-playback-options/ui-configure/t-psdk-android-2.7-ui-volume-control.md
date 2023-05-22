---
description: Du kan ställa in en gränssnittskontroll för att justera volymen för videon.
title: Ange volymkontroll
exl-id: 0daa87e2-51aa-4459-9a67-135dc54d09c7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Ange volymkontroll {#provide-volume-control}

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
