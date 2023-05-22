---
description: MediaPlayer-objektet representerar din mediespelare. Ett MediaPlayerItem representerar ljud eller video i spelaren.
title: Om klassen MediaPlayerItem
exl-id: ff7011ae-57d7-41e1-98be-5319bdc6f799
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Om klassen MediaPlayerItem{#about-the-mediaplayeritem-class}

MediaPlayer-objektet representerar din mediespelare. Ett MediaPlayerItem representerar ljud eller video i spelaren.

<!--<a id="section_01BC89E5C5A94D0A95EF9D29FBCE758A"></a>-->

När en medieresurs har lästs in skapas en instans av `MediaPlayerItem` klass som ger åtkomst till den resursen.

The `MediaResource` representerar en begäran som skickas av programlagret till `MediaPlayer` -instans för att läsa in innehåll.

The `MediaPlayer` löser medieresursen, läser in den associerade manifestfilen och tolkar manifestet. Detta är den asynkrona delen av resursinläsningsprocessen. The `MediaPlayerItem` instansen skapas när resursen har lösts och instansen är en löst version av en `MediaResource`. TVSDK ger åtkomst till nyskapade `MediaPlayerItem` instansen through `MediaPlayer.currentItem`.

>[!TIP]
>
>Du måste vänta tills resursen har lästs in innan du kan komma åt mediespelarobjektet.
