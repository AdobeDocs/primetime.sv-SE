---
seo-title: Licensens cachelagringstid
title: Licensens cachelagringstid
uuid: d448aa43-8cba-4b1d-8609-0dba4bb67042
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Licensens cachelagringstid{#license-caching-duration}

Licensens cachelagringstid anger hur länge en licens kan cachelagras på disken i klientens lokala License Store utan att licensservern behöver hämtas igen. Du kan också ange ett absolut datum och en absolut tidpunkt efter vilken en licens inte längre kan cachas.

När cachens förfallodatum har passerat är licensen inte längre giltig och klienten måste begära en ny licens från licensservern.

Exempel: Använd licensens cachelagringstid för att ange en fast tidsperiod som är giltig för en viss licens, t.ex. vid uthyrning. Du kan ange en 30-dagars uthyrning (med cache-lagring av licenser) för att ange den totala licenstiden för innehållet.
