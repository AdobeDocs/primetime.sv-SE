---
title: Licensens cachelagringstid
description: Licensens cachelagringstid
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Licensens cachelagringstid{#license-caching-duration}

Anger hur länge en licens kan cachas på disken i klientens lokala License Store utan att licensservern behöver hämtas igen. Du kan också ange ett absolut datum/tid efter vilket en licens inte längre kan cachas.

När cachens förfallodatum har passerat är licensen inte längre giltig och klienten måste begära en ny licens från licensservern.

Exempel: Använd licensens cachelagringstid för att ange en fast tidsperiod som är giltig för en viss licens, t.ex. vid uthyrning. En 30-dagars uthyrning kan anges (med cache-lagring av licenser) för att ange den totala licenstiden inom vilken innehållet ska konsumeras.
