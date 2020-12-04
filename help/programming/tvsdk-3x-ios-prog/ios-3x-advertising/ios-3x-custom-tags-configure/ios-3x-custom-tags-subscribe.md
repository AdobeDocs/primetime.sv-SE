---
description: TVSDK förbereder PTTimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.
seo-description: TVSDK förbereder PTTimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.
seo-title: Prenumerera på egna taggar
title: Prenumerera på egna taggar
uuid: e47076b2-6184-4c20-bae4-ba7ae62cf198
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 1%

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
