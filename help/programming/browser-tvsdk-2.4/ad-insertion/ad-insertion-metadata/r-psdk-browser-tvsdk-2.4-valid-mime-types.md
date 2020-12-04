---
description: En annons kan ha flera kreativa alternativ, varav en kan spelas upp.
seo-description: En annons kan ha flera kreativa alternativ, varav en kan spelas upp.
seo-title: Giltiga MIME-typer
title: Giltiga MIME-typer
uuid: ab2baac9-a9ef-44f1-83a1-2e6e471e3231
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Giltiga MIME-typer{#valid-mime-types}

En annons kan ha flera kreativa alternativ, varav en kan spelas upp.

Med MIME-typer kan du ange vilka typer av kreativa användare som kan prioriteras. De MIME-typer som anges av användare och de MIME-typer som stöds av Browser TVSDK används för att avgöra vilken kreativitet som ska prioriteras.

Så här anger du giltiga MIME-typer i Browser TVSDK:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

där `mimeTypes` är en array med strängar, och varje sträng representerar en MIME-typ.

Om flera mediefiler returneras för en annons beror valet på i vilken ordning mediefilerna visas i `validMimeTypes`-arrayen. De MIME-typer som har lägre index ges en inställning framför de som har högre index.
