---
description: Du kan ange en gränssnittskontroll för ljudvolymen.
seo-description: Du kan ange en gränssnittskontroll för ljudvolymen.
seo-title: Ange volymkontroll
title: Ange volymkontroll
uuid: 63e96424-54d0-4c16-bd94-2366722f752a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Ange volymkontroll{#provide-volume-control}

Du kan ange en gränssnittskontroll för ljudvolymen.

1. Vänta tills MediaPlayer-instansen har ett giltigt tillstånd för det här kommandot, vilket är vilket som helst förutom RELEASED eller ERROR.
1. Anropa `setVolume` på `MediaPlayer` instansen för att ställa in ljudvolymen.

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   Värdet för volymen representerar den begärda volymen uttryckt som en del av den maximala volymen, där 0 är tyst och 100 är den maximala volymen.

