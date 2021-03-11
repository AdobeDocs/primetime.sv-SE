---
description: Du kan ange en gränssnittskontroll för ljudvolymen.
title: Ange volymkontroll
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '87'
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

