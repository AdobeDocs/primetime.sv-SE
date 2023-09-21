---
description: Du kan ange en gränssnittskontroll för ljudvolymen.
title: Tillhandahåll volymkontroll
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# Tillhandahåll volymkontroll{#provide-volume-control}

Du kan ange en gränssnittskontroll för ljudvolymen.

1. Vänta tills MediaPlayer-instansen har ett giltigt tillstånd för det här kommandot, vilket är vilket som helst förutom RELEASED eller ERROR.
1. Utlysning `setVolume` på `MediaPlayer` -instans för att ange ljudvolymen.

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   Värdet för volymen representerar den begärda volymen uttryckt som en del av den maximala volymen, där 0 är tyst och 100 är den maximala volymen.
