---
description: MediaPlayer-objektet representerar din mediespelare. Ett MediaPlayerItem representerar ljud eller video i spelaren.
seo-description: MediaPlayer-objektet representerar din mediespelare. Ett MediaPlayerItem representerar ljud eller video i spelaren.
seo-title: Om klassen MediaPlayerItem
title: Om klassen MediaPlayerItem
uuid: d7f65edf-4693-4b1e-bae0-46fadce98751
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Om klassen MediaPlayerItem{#about-the-mediaplayeritem-class}

MediaPlayer-objektet representerar din mediespelare. Ett MediaPlayerItem representerar ljud eller video i spelaren.

När en medieresurs har lästs in, skapar TVSDK en instans av `MediaPlayerItem` klassen som ger åtkomst till den resursen.

Detta `MediaResource` representerar en begäran som skickas av programlagret till `MediaPlayer` instansen för att läsa in innehåll.

Medieresursen `MediaPlayer` åtgärdas, den tillhörande manifestfilen läses in och manifestet tolkas. Detta är den asynkrona delen av resursinläsningsprocessen. Instansen `MediaPlayerItem` skapas när resursen har lösts och den här instansen är en löst version av en `MediaResource`. TVSDK ger åtkomst till den nya `MediaPlayerItem` instansen via `MediaPlayer.CurrentItem`

>[!TIP]
>
>Du måste vänta tills resursen har lästs in innan du kan komma åt mediespelarobjektet.

