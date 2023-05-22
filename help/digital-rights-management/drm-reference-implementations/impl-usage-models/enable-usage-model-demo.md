---
title: Aktivera demo av användningsmodell
description: Aktivera demo av användningsmodell
copied-description: true
exl-id: 5d546f1a-ebf6-4c93-9a73-fa812cd71086
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---

# Aktivera demo av användningsmodell{#enable-the-usage-model-demo}

1. Ange den anpassade egenskapen `RI_UsageModelDemo=true` vid paketeringstid.

   Om du paketerar innehåll med kommandoradsverktyget för Media Packager anger du:

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>Om du inte aktiverar det valfria demoläget vid paketering utfärdar licensservern en licens baserad på den första giltiga DRM-principen som bearbetas.
