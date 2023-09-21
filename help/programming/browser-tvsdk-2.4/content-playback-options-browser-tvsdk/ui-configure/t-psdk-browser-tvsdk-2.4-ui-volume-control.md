---
description: Du kan ange en gränssnittskontroll för ljudvolymen.
title: Tillhandahåll volymkontroll
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 0%

---

# Tillhandahåll volymkontroll{#provide-volume-control}

Du kan ange en gränssnittskontroll för ljudvolymen.

1. Vänta på `MediaPlayer` -instansen är i ett giltigt tillstånd för det här kommandot.

   Alla tillstånd utom FRISLÄPPT eller FEL är giltiga.
1. Ange volymattributet på `MediaPlayer` -instans för att ange ljudvolymen.

   ```js
   player.volume = ...
   ```

   Värdet för volymen representerar den begärda volymen uttryckt som en del av den maximala volymen, där 0 är tyst och är den maximala volymen.
