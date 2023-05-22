---
title: Anpassade metadata
description: Anpassade metadata
copied-description: true
exl-id: d7783420-b345-44de-8f22-a16dda5d7554
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Anpassade metadata {#custom-metadata}

**Ange en anpassad nyckel/värde som ska läggas till i innehållsmetadata som kan tolkas av serverprogrammet.**

Med innehållsmetadataformatet Adobe Access kan anpassade nyckel-/värdepar vid paketeringstid inkluderas, vilket kan bearbetas av licensservern under licensutfärdandet. Dessa metadata är åtskilda från principen och kan vara unika för varje del av innehållet.

Exempel: Under en betafas inkluderar du den anpassade egenskapen&quot;Release:BETA&quot; vid paketeringen. Licensservrar kan leverera licenser till det här innehållet under betaperioden, men när betaperioden har löpt ut tillåter inte licensservrarna åtkomst till innehållet.
