---
description: Browser TVSDK innehåller verktyg för att skapa ett avancerat videospelarprogram (din Primetime-spelare) som du kan integrera med andra Primetime-komponenter.
seo-description: Browser TVSDK innehåller verktyg för att skapa ett avancerat videospelarprogram (din Primetime-spelare) som du kan integrera med andra Primetime-komponenter.
seo-title: 'null'
title: 'null'
uuid: 57b35a5f-87f8-41a2-ad85-300b999dc30b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Flash-redundans {#flash-failover}

Browser TVSDK innehåller verktyg för att skapa ett avancerat videospelarprogram (din Primetime-spelare) som du kan integrera med andra Primetime-komponenter.

Använd plattformens verktyg för att skapa en spelare och ansluta den till mediespelarvyn i Browser TVSDK, som har metoder för att spela upp och hantera videoklipp. Browser TVSDK innehåller till exempel metoderna play och pause. Du kan skapa användargränssnittsknappar på din plattform och ställa in knapparna för att anropa dessa webbläsares TVSDK-metoder.

## Flash fallback {#section_92D3884A13A6431F9A9CC5C79715D888}

I Browser TVSDK interagerar ditt program bara med `Primetime.js` API:t. Den underliggande implementeringen av Browser TVSDK avgör vilken spelarteknologi som ska användas baserat på den aktuella plattformen och resurstypen för de media som ska spelas upp.

Beslutet om spelartekniken fattas inte förrän du anropar `MediaPlayer.replaceCurrentResource` för att spela en viss resurs.

Exempel:

```js
var player = new AdobePSDK.MediaPlayer(), 
              mediaResource = new AdobePSDK.MediaResource(url, 
              AdobePSDK.MediaResource.Type.TYPE_HLS); 
              ... 
              player.replaceCurrentResource(mediaResource);
```

## Ange vilken mediespelare som ska användas {#section_D844E386AF5848688D204DEE258ECEE6}

Detta exempel visar processen att fastställa spelartekniken:

>[!TIP]
>
>Processen kan variera beroende på webbadressen och miljön.

1. Om Media Source Extensions stöds kan du använda det utan några kända begränsningar.
1. Använd taggen direkt utan MSE om den stöds `<video>` .
1. Kontrollera att du använder minst Adobe Flash Player version 23.0.
1. Om ingen lämplig uppspelningsteknik hittas returneras ett fel `replaceCurrentResource` .

Ett efterföljande `replaceCurrentResource` anrop till samma `MediaPlayer` instans följer samma process. På så sätt kan du spela upp olika resurstyper med samma `MediaPlayer` instans i samma överordnade `<DIV>` -tagg som du angav när `MediaPlayerView` instansen skapades.

>[!TIP]
>
>SWF-objektet och `<video>` -taggen kapslas i den överordnade `<DIV>` taggen.

