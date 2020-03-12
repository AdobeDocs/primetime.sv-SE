---
description: TVSDK förbereder TimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.
seo-description: TVSDK förbereder TimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.
seo-title: Prenumerera på egna taggar
title: Prenumerera på egna taggar
uuid: f1a934bd-772e-435f-84b5-cb48db23c06e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Prenumerera på egna taggar {#subscribe-to-custom-tags}

TVSDK förbereder TimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.

Innan uppspelningen startar måste du prenumerera på taggarna. För att få meddelanden om anpassade taggar i HLS-manifestationer:

1. Ange egna annonstaggnamn globalt genom att skicka en array som innehåller de anpassade taggar som ska `setSubscribedTags` anges `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >Du måste ta med prefixet `#` när du arbetar med HLS-strömmar.

   Exempel:

   ```java
   String[] array = new String[3]; 
   array[0] = "#EXT-X-ASSET"; 
   array[1] = "#EXT-X-BLACKOUT"; 
   array[2] = "#EXT-OATCLS-SCTE35"; 
   MediaPlayerItemConfig.setSubscribedTags(array);
   ```
