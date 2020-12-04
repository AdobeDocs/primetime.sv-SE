---
description: 'null'
seo-description: 'null'
seo-title: Spela upp automatiskt på iOS
title: Spela upp automatiskt på iOS
uuid: d15bad24-be50-49e5-90f4-68dbda96fb6d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Spela upp automatiskt på iOS{#autoplay-on-ios}

Implementeringen av volym-API:t för AdobePSDK.MediaPlayer tillåter automatisk uppspelning av innehåll på enheter som kör iOS version 10 eller senare. iOS tillåter endast automatisk uppspelning när volymen är avstängd. När volymen är inställd på noll ställer API:t in egenskapen `muted` för videotaggen på `true`, annars är egenskapen `muted` inställd på `false`. API:t `play` startar uppspelningen utan någon användarinteraktion eller användargest.

För automatisk uppspelning på iPhone anger du dessutom `playsInline`-egenskapen för taggen `video` till `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>Om du använder egenskapen `playsInline` startas uppspelningen utan helskärmsläge.

