---
description: Browser TVSDK innehåller verktyg för att skapa ett avancerat videospelarprogram (din Primetime-spelare) som du kan integrera med andra Primetime-komponenter.
title: Redundans för Flash
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Redundans för Flash {#flash-failover}

Browser TVSDK innehåller verktyg för att skapa ett avancerat videospelarprogram (din Primetime-spelare) som du kan integrera med andra Primetime-komponenter.

Använd plattformens verktyg för att skapa en spelare och ansluta den till mediespelarvyn i Browser TVSDK, som har metoder för att spela upp och hantera videoklipp. Browser TVSDK innehåller till exempel metoderna play och pause. Du kan skapa användargränssnittsknappar på din plattform och ställa in knapparna för att anropa dessa webbläsares TVSDK-metoder.

## Flash fallback {#section_92D3884A13A6431F9A9CC5C79715D888}

I Browser TVSDK interagerar ditt program bara med `Primetime.js` API. Den underliggande implementeringen av Browser TVSDK avgör vilken spelarteknologi som ska användas baserat på den aktuella plattformen och resurstypen för de media som ska spelas upp.

Beslutet om spelartekniken fattas inte förrän du ringer `MediaPlayer.replaceCurrentResource` för att spela upp en specifik resurs.

Till exempel:

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
1. Om det stöds använder du `<video>` -taggen direkt utan MSE.
1. Kontrollera att du använder minst Adobe Flash Player version 23.0.
1. Om ingen lämplig uppspelningsteknik hittas `replaceCurrentResource` returnerar ett fel.

En efterföljande `replaceCurrentResource` ring på samma `MediaPlayer` -instansen följer samma process. På så sätt kan du spela upp olika resurstyper med samma `MediaPlayer` instans i samma överordnade `<DIV>` -taggen som du angav när `MediaPlayerView` -instansen skapades.

>[!TIP]
>
>Objektet SWF och `<video>` -taggen är kapslad i den överordnade `<DIV>` -tagg.
