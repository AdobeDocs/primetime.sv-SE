---
description: Du kan ange en gränssnittskontroll för ljudvolymen.
title: Ange volymkontroll
exl-id: 5c446081-5491-46b6-9259-293131af80cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 0%

---

# Ange volymkontroll{#provide-volume-control}

Du kan ange en gränssnittskontroll för ljudvolymen.

1. Vänta på `MediaPlayer` -instansen är i ett giltigt tillstånd för det här kommandot.

   Alla tillstånd utom FRISLÄPPT eller FEL är giltiga.
1. Ange volymattributet på `MediaPlayer` -instans för att ange ljudvolymen.

   ```js
   player.volume = ...
   ```

   Värdet för volymen representerar den begärda volymen uttryckt som en del av den maximala volymen, där 0 är tyst och är den maximala volymen.
