---
title: Aktivera demo av användningsmodell
description: Aktivera demo av användningsmodell
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
