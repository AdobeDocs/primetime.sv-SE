---
description: Du kan åsidosätta standardbeteendet för hur TVSDK hanterar sökningar efter annonser när du använder anpassade annonsmarkörer.
title: Styra uppspelningsbeteendet för sökning efter anpassade annonsmarkörer
exl-id: 5c17809b-f78b-49f7-85a4-9072502f4a24
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Styra uppspelningsbeteendet för sökning efter anpassade annonsmarkörer {#control-playback-behavior-for-seeking-over-custom-ad-markers}

Du kan åsidosätta standardbeteendet för hur TVSDK hanterar sökningar efter annonser när du använder anpassade annonsmarkörer.

Som standard hoppas annonserna över av TVSDK när en användare söker i eller förbi annonsavsnitt som är ett resultat av placeringen av anpassade annonsmärken. Detta kan skilja sig från det aktuella uppspelningsbeteendet för standardannonsbrytningar. Du kan ställa in TVSDK så att spelhuvudet flyttas till början av den senast hoppade anpassade annonsen när användaren söker efter en eller flera anpassade annonser.

1. Utlysning `CustomRangeMetadata.setAdjustSeekPosition` med `true`.

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. Använd `customRangeMetadata` in `MediaPlayerItemConfig`.

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```
