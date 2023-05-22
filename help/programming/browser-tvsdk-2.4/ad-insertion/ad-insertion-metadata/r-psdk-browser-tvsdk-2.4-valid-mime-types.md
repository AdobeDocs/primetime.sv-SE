---
description: En annons kan ha flera kreativa alternativ, varav en kan spelas upp.
title: Giltiga MIME-typer
exl-id: 878cae20-2a94-4795-8908-be7daffefb41
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '138'
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

Om flera mediefiler returneras för en annons beror valet på i vilken ordning mediefilerna visas i `validMimeTypes` array. De MIME-typer som har lägre index ges en inställning framför de som har högre index.
