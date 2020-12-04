---
description: Browser TVSDK innehåller verktyg för att skapa ett avancerat videospelarprogram (din Primetime-spelare) som du kan integrera med andra Primetime-komponenter.
seo-description: Browser TVSDK innehåller verktyg för att skapa ett avancerat videospelarprogram (din Primetime-spelare) som du kan integrera med andra Primetime-komponenter.
seo-title: 'null'
title: 'null'
uuid: 57b35a5f-87f8-41a2-ad85-300b999dc30b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Redundans för Flash {#flash-failover}

Browser TVSDK innehåller verktyg för att skapa ett avancerat videospelarprogram (din Primetime-spelare) som du kan integrera med andra Primetime-komponenter.

Använd plattformens verktyg för att skapa en spelare och ansluta den till mediespelarvyn i Browser TVSDK, som har metoder för att spela upp och hantera videoklipp. Browser TVSDK innehåller till exempel metoderna play och pause. Du kan skapa användargränssnittsknappar på din plattform och ställa in knapparna för att anropa dessa webbläsares TVSDK-metoder.

## Flash fallback {#section_92D3884A13A6431F9A9CC5C79715D888}

I Browser TVSDK interagerar ditt program bara med API:t `Primetime.js`. Den underliggande implementeringen av Browser TVSDK avgör vilken spelarteknologi som ska användas baserat på den aktuella plattformen och resurstypen för de media som ska spelas upp.

Spelartekniken används inte förrän du ringer `MediaPlayer.replaceCurrentResource` för att spela upp en viss resurs.

Exempel:

```js
var player = new AdobePSDK.MediaPlayer(), 
              mediaResource = new AdobePSDK.MediaResource(url, 
              AdobePSDK.MediaResource.Type.TYPE_HLS); 
              ... 
              player.replaceCurrentResource(mediaResource);
```

## Fastställ vilken mediespelare som ska använda {#section_D844E386AF5848688D204DEE258ECEE6}

Detta exempel visar processen att fastställa spelartekniken:

>[!TIP]
>
>Processen kan variera beroende på webbadressen och miljön.

1. Om Media Source Extensions stöds kan du använda det utan några kända begränsningar.
1. Om det stöds kan du använda taggen `<video>` direkt utan MSE.
1. Kontrollera att du använder minst Adobe Flash Player version 23.0.
1. Om ingen lämplig uppspelningsteknik hittas returnerar `replaceCurrentResource` ett fel.

Ett efterföljande `replaceCurrentResource`-anrop på samma `MediaPlayer`-instans följer samma process. Detta gör att du kan spela upp olika resurstyper genom att använda samma `MediaPlayer`-instans i samma överordnade `<DIV>`-tagg som du angav när `MediaPlayerView`-instansen skapades.

>[!TIP]
>
>SWF-objektet och `<video>`-taggen är kapslade i den överordnade `<DIV>`-taggen.

