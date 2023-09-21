---
title: Spela upp automatiskt på iOS
description: Spela upp automatiskt på iOS
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# Spela upp automatiskt på iOS{#autoplay-on-ios}

Implementeringen av volym-API:t för AdobePSDK.MediaPlayer tillåter automatisk uppspelning av innehåll på enheter som kör iOS version 10 eller senare. iOS tillåter endast automatisk uppspelning när volymen är avstängd. När volymen är inställd på noll anger API:t `muted` egenskapen för videotaggen till `true`, annars `muted` egenskapen är inställd på `false`. The `play` API startar uppspelningen utan någon användarinteraktion eller användargest.

För automatisk uppspelning på iPhone anger du dessutom `playsInline` egenskapen för `video` tagga till `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>Användning av `playsInline` egenskapen startar uppspelningen utan helskärmsläge.
