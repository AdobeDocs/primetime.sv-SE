---
seo-title: Aktivera demo av användningsmodell
title: Aktivera demo av användningsmodell
uuid: 43930ebb-e936-4f48-990d-7ad19992e326
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# Aktivera demo av användningsmodell{#enable-the-usage-model-demo}

1. Ange den anpassade egenskapen `RI_UsageModelDemo=true` vid paketering.

   Om du paketerar innehåll med kommandoradsverktyget för Media Packager anger du:

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>Om du inte aktiverar det valfria demoläget vid paketering utfärdar licensservern en licens baserad på den första giltiga DRM-principen som bearbetas.

