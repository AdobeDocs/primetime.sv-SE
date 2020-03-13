---
description: Du kan åsidosätta standardbeteendet för hur TVSDK hanterar sökningar efter annonser när du använder anpassade annonsmarkörer.
seo-description: Du kan åsidosätta standardbeteendet för hur TVSDK hanterar sökningar efter annonser när du använder anpassade annonsmarkörer.
seo-title: Styra uppspelningsbeteendet för sökning efter anpassade annonsmarkörer
title: Styra uppspelningsbeteendet för sökning efter anpassade annonsmarkörer
uuid: ec95a22f-0143-4c80-826f-d6b40e77cf26
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Styra uppspelningsbeteendet för sökning efter anpassade annonsmarkörer {#control-playback-behavior-for-seeking-over-custom-ad-markers}

Du kan åsidosätta standardbeteendet för hur TVSDK hanterar sökningar efter annonser när du använder anpassade annonsmarkörer.

Som standard hoppas annonserna över av TVSDK när en användare söker i eller förbi annonsavsnitt som är ett resultat av placeringen av anpassade annonsmärken. Detta kan skilja sig från det aktuella uppspelningsbeteendet för standardannonsbrytningar. Du kan ställa in TVSDK så att spelhuvudet flyttas till början av den senast hoppade anpassade annonsen när användaren söker efter en eller flera anpassade annonser.

1. Ring `CustomRangeMetadata.setAdjustSeekPosition` med `true`.

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. Använd `customRangeMetadata` i `MediaPlayerItemConfig`.

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```
