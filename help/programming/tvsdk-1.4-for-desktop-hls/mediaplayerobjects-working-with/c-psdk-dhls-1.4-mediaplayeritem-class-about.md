---
description: MediaPlayer-objektet representerar din mediespelare. Ett MediaPlayerItem representerar ljud eller video i spelaren.
seo-description: MediaPlayer-objektet representerar din mediespelare. Ett MediaPlayerItem representerar ljud eller video i spelaren.
seo-title: Om klassen MediaPlayerItem
title: Om klassen MediaPlayerItem
uuid: 531dd1a6-d72c-4ae3-9c3f-2f1d854245c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Om klassen MediaPlayerItem{#about-the-mediaplayeritem-class}

MediaPlayer-objektet representerar din mediespelare. Ett MediaPlayerItem representerar ljud eller video i spelaren.

<!--<a id="section_01BC89E5C5A94D0A95EF9D29FBCE758A"></a>-->

När en medieresurs har lästs in, skapar TVSDK en instans av `MediaPlayerItem` klassen som ger åtkomst till den resursen.

Detta `MediaResource` representerar en begäran som skickas av programlagret till `MediaPlayer` instansen för att läsa in innehåll.

Medieresursen `MediaPlayer` åtgärdas, den tillhörande manifestfilen läses in och manifestet tolkas. Detta är den asynkrona delen av resursinläsningsprocessen. Instansen `MediaPlayerItem` skapas när resursen har lösts och den här instansen är en löst version av en `MediaResource`. TVSDK ger åtkomst till den nyligen skapade `MediaPlayerItem` instansen via `MediaPlayer.currentItem`.

>[!TIP]
>
>Du måste vänta tills resursen har lästs in innan du kan komma åt mediespelarobjektet.

