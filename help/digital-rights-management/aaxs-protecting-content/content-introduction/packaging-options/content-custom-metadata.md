---
title: Anpassade metadata
description: Anpassade metadata
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# Anpassade metadata {#custom-metadata}

**Ange en anpassad nyckel/värde som ska läggas till i innehållsmetadata som kan tolkas av serverprogrammet.**

Med innehållsmetadataformatet Adobe Access kan anpassade nyckel-/värdepar vid paketeringstid inkluderas, vilket kan bearbetas av licensservern under licensutfärdandet. Dessa metadata är åtskilda från principen och kan vara unika för varje del av innehållet.

Exempel: Under en betafas inkluderar du den anpassade egenskapen&quot;Release:BETA&quot; vid paketeringen. Licensservrar kan leverera licenser till det här innehållet under betaperioden, men när betaperioden har löpt ut tillåter inte licensservrarna åtkomst till innehållet.
