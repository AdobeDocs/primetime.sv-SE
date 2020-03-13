---
description: TVSDK förbereder PTTimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.
seo-description: TVSDK förbereder PTTimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.
seo-title: Prenumerera på egna taggar
title: Prenumerera på egna taggar
uuid: de66d3db-46d1-485f-9d3a-6e28495bfb13
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Prenumerera på egna taggar {#subscribe-to-custom-tags}

TVSDK förbereder PTTimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.

Innan uppspelningen startar måste du prenumerera på taggarna.
För att få meddelanden om anpassade taggar i HLS-manifestationer:

1. Ange egna annonstaggnamn globalt genom att skicka en array som innehåller de anpassade taggar som ska `setSubscribedTags` anges `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >Du måste ta med prefixet `#` när du arbetar med HLS-strömmar.

   Exempel:

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```

