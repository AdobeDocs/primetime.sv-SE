---
description: När en MediaResource har lästs in, skapar webbläsaren TVSDK en instans av klassen MediaPlayerItem som ger åtkomst till resursen.
seo-description: När en MediaResource har lästs in, skapar webbläsaren TVSDK en instans av klassen MediaPlayerItem som ger åtkomst till resursen.
seo-title: Om klassen MediaPlayerItem
title: Om klassen MediaPlayerItem
uuid: 5226d3ad-2438-44fe-a8ef-bcc0da8331b8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Om klassen MediaPlayerItem{#about-the-mediaplayeritem-class}

När en MediaResource har lästs in, skapar webbläsaren TVSDK en instans av klassen MediaPlayerItem som ger åtkomst till resursen.

`MediaResource` representerar en begäran som skickas av programlagret till `MediaPlayer`-instansen för att läsa in innehåll.

`MediaPlayer` löser medieresursen, läser in den associerade manifestfilen och tolkar manifestet. Detta är den asynkrona delen av resursinläsningsprocessen. `MediaPlayerItem`-instansen skapas när resursen har lösts och den här instansen är en löst version av `MediaResource`. Webbläsarens TVSDK ger åtkomst till den nyligen skapade `MediaPlayerItem`-instansen via `MediaPlayer.CurrentItem`.

>[!TIP]
>
>Du måste vänta tills resursen har lästs in innan du kan komma åt mediespelarobjektet.

