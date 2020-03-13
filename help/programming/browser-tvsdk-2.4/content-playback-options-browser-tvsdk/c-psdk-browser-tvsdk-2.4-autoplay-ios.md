---
description: 'null'
seo-description: 'null'
seo-title: Spela upp automatiskt på iOS
title: Spela upp automatiskt på iOS
uuid: d15bad24-be50-49e5-90f4-68dbda96fb6d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Spela upp automatiskt på iOS{#autoplay-on-ios}

Implementeringen av volym-API:t för AdobePSDK.MediaPlayer tillåter automatisk uppspelning av innehåll på enheter som kör iOS version 10 eller senare. iOS tillåter endast automatisk uppspelning när volymen är avstängd. När volymen är inställd på noll ställer API:t in videotaggens `muted` egenskap på `true`, annars ställs `muted` egenskapen in på `false`. API:t startar `play` uppspelningen utan någon användarinteraktion eller användargest.

För automatisk uppspelning på iPhone anger du dessutom egenskapen `playsInline` för `video` -taggen till `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>När du använder egenskapen startas uppspelningen utan helskärmsläge. `playsInline`

