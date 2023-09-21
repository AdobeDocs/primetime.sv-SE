---
description: TVSDK förbereder PTTimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.
title: Prenumerera på egna taggar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Prenumerera på egna taggar {#subscribe-to-custom-tags}

TVSDK förbereder PTTimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.

Innan uppspelningen startar måste du prenumerera på taggarna.
För att få meddelanden om anpassade taggar i HLS-manifestationer:

1. Ange egna annonstaggnamn globalt genom att skicka en array som innehåller de anpassade taggarna till `setSubscribedTags` in `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >Du måste inkludera `#` när du arbetar med HLS-strömmar.

   Till exempel:

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```
