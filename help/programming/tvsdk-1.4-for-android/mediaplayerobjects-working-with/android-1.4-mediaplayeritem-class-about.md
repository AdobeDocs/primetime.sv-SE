---
description: MediaPlayer-objektet representerar din mediespelare. Ett MediaPlayerItem representerar ljud eller video i spelaren.
title: Om klassen MediaPlayerItem
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Om klassen MediaPlayerItem{#about-the-mediaplayeritem-class}

MediaPlayer-objektet representerar din mediespelare. Ett MediaPlayerItem representerar ljud eller video i spelaren.

När en medieresurs har lästs in skapas en instans av `MediaPlayerItem` klass som ger åtkomst till den resursen.

The `MediaResource` representerar en begäran som skickas av programlagret till `MediaPlayer` -instans för att läsa in innehåll.

The `MediaPlayer` löser medieresursen, läser in den associerade manifestfilen och tolkar manifestet. Detta är den asynkrona delen av resursinläsningsprocessen. The `MediaPlayerItem` instansen skapas när resursen har lösts och instansen är en löst version av en `MediaResource`. TVSDK ger åtkomst till nyskapade `MediaPlayerItem` instansen through `MediaPlayer.CurrentItem`

>[!TIP]
>
>Du måste vänta tills resursen har lästs in innan du kan komma åt mediespelarobjektet.
