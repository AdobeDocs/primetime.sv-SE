---
description: TVSDK förbereder PTTimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.
title: Prenumerera på egna taggar
exl-id: 85d13ae1-d33c-4394-b9fa-a66024974c8d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
   >Du måste inkludera `#` prefix när du arbetar med HLS-strömmar.

   Till exempel:

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```
