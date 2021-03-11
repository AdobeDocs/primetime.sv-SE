---
description: Klassen PlayerFragment är den plats där du redigerar koden för att skapa de fullständigt aktiverade funktionshanterarna.
title: PlayerFragment
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# PlayerFragment {#playerfragment}

Klassen PlayerFragment är den plats där du redigerar koden för att skapa de fullständigt aktiverade funktionshanterarna.

Klassen `PlayerFragment` innehåller alla UI-komponenter som `playerFrame`, `ControlBar`, `playerClickableAdFragment` och `adOverlay`.

Den hanterar initieringen av alla dessa komponenter samt skapar spelaren, ställer in vyer, skapar funktionshanterare för mediespelaren, hanterar mediahändelser som resume, play och pause och hanterar händelseavlyssnarna för `QoSManager`, `DRMManager`, `CCManager`, `AAManager`, `AdsManager`, `PlaybackManager` och `EntitlementManager`.

XML-filen som innehåller konfigurationsparametrarna för `PlayerFragment` är `res/layout/fragment_player.xml`.

Innan du skapar funktionshanterarna måste du skapa mediespelaren genom att kontrollera att följande kod finns i `PlayerFragment.java`-filen:

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
