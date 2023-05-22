---
description: När en MediaResource har lästs in, skapar webbläsaren TVSDK en instans av klassen MediaPlayerItem som ger åtkomst till resursen.
title: Om klassen MediaPlayerItem
exl-id: 6e47914c-3d46-4aaf-9144-1a00d886e5bf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
