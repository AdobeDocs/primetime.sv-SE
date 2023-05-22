---
description: Du kan ange en gränssnittskontroll för ljudvolymen.
title: Ange volymkontroll
exl-id: aa8ffdf3-515b-4899-8a00-8fb5b8c595a9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# Ange volymkontroll{#provide-volume-control}

Du kan ange en gränssnittskontroll för ljudvolymen.

1. Vänta tills MediaPlayer-instansen har ett giltigt tillstånd för det här kommandot, vilket är vilket som helst förutom RELEASED eller ERROR.
1. Utlysning `setVolume` på `MediaPlayer` -instans för att ange ljudvolymen.

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   Värdet för volymen representerar den begärda volymen uttryckt som en del av den maximala volymen, där 0 är tyst och 100 är den maximala volymen.
