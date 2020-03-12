---
description: När du har läst in MediaResource-objektet skapar TVSDK en instans av MediaPlayerItem-klassen som ger åtkomst till resursen.
seo-description: När du har läst in MediaResource-objektet skapar TVSDK en instans av MediaPlayerItem-klassen som ger åtkomst till resursen.
seo-title: Om klassen MediaPlayerItem
title: Om klassen MediaPlayerItem
uuid: 2d37f358-d158-481b-81d5-27546e9c2e0e
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Om klassen MediaPlayerItem {#about-the-mediaplayeritem-class}

MediaPlayer-objektet representerar din mediespelare. Ett MediaPlayerItem representerar ljud eller video i spelaren.

När du har läst in MediaResource-objektet skapar TVSDK en instans av MediaPlayerItem-klassen som ger åtkomst till resursen.

Detta `MediaResource` representerar en begäran som skickas av programlagret till `MediaPlayer` instansen för att läsa in innehåll.

Medieresursen `MediaPlayer` åtgärdas, den tillhörande manifestfilen läses in och manifestet tolkas. Detta är den asynkrona delen av resursinläsningsprocessen. Instansen `MediaPlayerItem` skapas när resursen har lösts och den här instansen är en löst version av en `MediaResource`. TVSDK ger åtkomst till den nyligen skapade `MediaPlayerItem` instansen via `MediaPlayer.CurrentItem`.

>[!TIP]
>
>Du måste vänta tills resursen har lästs in innan du kan komma åt mediespelarobjektet.