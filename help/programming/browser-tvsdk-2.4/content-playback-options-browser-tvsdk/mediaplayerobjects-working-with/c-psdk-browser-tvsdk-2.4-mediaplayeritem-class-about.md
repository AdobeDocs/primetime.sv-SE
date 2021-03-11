---
description: När en MediaResource har lästs in, skapar webbläsaren TVSDK en instans av klassen MediaPlayerItem som ger åtkomst till resursen.
title: Om klassen MediaPlayerItem
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# Om klassen MediaPlayerItem{#about-the-mediaplayeritem-class}

När en MediaResource har lästs in, skapar webbläsaren TVSDK en instans av klassen MediaPlayerItem som ger åtkomst till resursen.

`MediaResource` representerar en begäran som skickas av programlagret till `MediaPlayer`-instansen för att läsa in innehåll.

`MediaPlayer` löser medieresursen, läser in den associerade manifestfilen och tolkar manifestet. Detta är den asynkrona delen av resursinläsningsprocessen. `MediaPlayerItem`-instansen skapas när resursen har lösts och den här instansen är en löst version av `MediaResource`. Webbläsarens TVSDK ger åtkomst till den nyligen skapade `MediaPlayerItem`-instansen via `MediaPlayer.CurrentItem`.

>[!TIP]
>
>Du måste vänta tills resursen har lästs in innan du kan komma åt mediespelarobjektet.

