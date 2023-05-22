---
description: Klassen PlayerFragment är den plats där du redigerar koden för att skapa de fullständigt aktiverade funktionshanterarna.
title: PlayerFragment
exl-id: 9060f0f5-9148-48cd-b89b-718607dd70bc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# PlayerFragment {#playerfragment}

Klassen PlayerFragment är den plats där du redigerar koden för att skapa de fullständigt aktiverade funktionshanterarna.

The `PlayerFragment` -klassen innehåller alla UI-komponenter som `playerFrame`, `ControlBar`, `playerClickableAdFragment`och `adOverlay`.

Den hanterar initieringen av alla dessa komponenter samt skapar spelaren, ställer in vyer, skapar funktionshanterare för mediespelaren, hanterar mediahändelser som resume, play, pause och hanterar händelseavlyssnare för `QoSManager`, `DRMManager`, `CCManager`, `AAManager`, `AdsManager`, `PlaybackManager`och `EntitlementManager`.

XML-filen som innehåller konfigurationsparametrarna för `PlayerFragment` är `res/layout/fragment_player.xml`.

Innan du skapar funktionshanterarna måste du skapa mediespelaren genom att kontrollera att följande kod finns i `PlayerFragment.java` fil:

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
