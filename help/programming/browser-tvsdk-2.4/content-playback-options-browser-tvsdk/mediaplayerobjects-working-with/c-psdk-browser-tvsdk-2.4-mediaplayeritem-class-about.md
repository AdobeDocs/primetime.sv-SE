---
description: När en MediaResource har lästs in, skapar webbläsaren TVSDK en instans av klassen MediaPlayerItem som ger åtkomst till resursen.
title: Om klassen MediaPlayerItem
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# Om klassen MediaPlayerItem{#about-the-mediaplayeritem-class}

När en MediaResource har lästs in, skapar webbläsaren TVSDK en instans av klassen MediaPlayerItem som ger åtkomst till resursen.

The `MediaResource` representerar en begäran som skickas av programlagret till `MediaPlayer` -instans för att läsa in innehåll.

The `MediaPlayer` löser medieresursen, läser in den associerade manifestfilen och tolkar manifestet. Detta är den asynkrona delen av resursinläsningsprocessen. The `MediaPlayerItem` instansen skapas när resursen har lösts och instansen är en löst version av en `MediaResource`. Webbläsarens TVSDK ger åtkomst till den nyskapade `MediaPlayerItem` instansen through `MediaPlayer.CurrentItem`.

>[!TIP]
>
>Du måste vänta tills resursen har lästs in innan du kan komma åt mediespelarobjektet.
