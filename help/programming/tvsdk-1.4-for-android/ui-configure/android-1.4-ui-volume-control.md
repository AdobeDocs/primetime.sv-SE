---
description: Du kan ange en gränssnittskontroll för ljudvolymen.
title: Ange volymkontroll
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# Ange volymkontroll{#provide-volume-control}

Du kan ange en gränssnittskontroll för ljudvolymen.

1. Vänta tills MediaPlayer-instansen har ett giltigt tillstånd för det här kommandot, vilket är vilket som helst förutom RELEASED eller ERROR.
1. Anropa `setVolume` på `MediaPlayer`-instansen för att ställa in ljudvolymen.

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   Värdet för volymen representerar den begärda volymen uttryckt som en del av den maximala volymen, där 0 är tyst och 100 är den maximala volymen.

