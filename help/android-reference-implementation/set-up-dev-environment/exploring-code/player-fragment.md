---
description: Klassen PlayerFragment är den plats där du redigerar koden för att skapa de fullständigt aktiverade funktionshanterarna.
seo-description: Klassen PlayerFragment är den plats där du redigerar koden för att skapa de fullständigt aktiverade funktionshanterarna.
seo-title: PlayerFragment
title: PlayerFragment
uuid: 83f02c31-f3b1-4d16-97c8-5b391e8c999a
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '134'
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
