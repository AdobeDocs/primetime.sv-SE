---
description: TVSDK förbereder PTTimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.
title: Prenumerera på egna taggar
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 2%

---


# Prenumerera på anpassade taggar {#subscribe-to-custom-tags}

TVSDK förbereder PTTimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.

Innan uppspelningen startar måste du prenumerera på taggarna.
För att få meddelanden om anpassade taggar i HLS-manifestationer:

1. Ange de anpassade annonstaggnamnen globalt genom att skicka en array som innehåller de anpassade taggarna till `setSubscribedTags` i `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >Du måste inkludera `#`-prefixet när du arbetar med HLS-strömmar.

   Exempel:

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```

