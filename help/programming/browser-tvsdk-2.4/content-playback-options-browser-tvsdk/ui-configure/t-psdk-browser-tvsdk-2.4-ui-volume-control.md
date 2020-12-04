---
description: Du kan ange en gränssnittskontroll för ljudvolymen.
seo-description: Du kan ange en gränssnittskontroll för ljudvolymen.
seo-title: Ange volymkontroll
title: Ange volymkontroll
uuid: 5f2f69cc-3969-4ca2-8ab9-5713fdf5cdb8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---


# Ange volymkontroll{#provide-volume-control}

Du kan ange en gränssnittskontroll för ljudvolymen.

1. Vänta tills `MediaPlayer`-instansen har ett giltigt tillstånd för det här kommandot.

   Alla tillstånd utom FRISLÄPPT eller FEL är giltiga.
1. Ställ in ljudvolymen genom att ställa in volymattributet på `MediaPlayer`-instansen.

   ```js
   player.volume = ...
   ```

   Värdet för volymen representerar den begärda volymen uttryckt som en del av den maximala volymen, där 0 är tyst och är den maximala volymen.

