---
description: 'null'
seo-description: 'null'
seo-title: Krav för annonsering
title: Krav för annonsering
uuid: 60e299df-4f42-455a-8983-8964f7a197e1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Krav för annonsering {#advertising-requirements}

Ni kan infoga annonser i ert VOD-innehåll och direktsänt/linjärt innehåll med hjälp av Adobe Primetime annonsbeslutsgränssnitt.

Primetimes annonsbeslut fungerar tillsammans med TVSDK för att identifiera annonsmöjligheter, lösa annonser och infoga lösta annonser i era videoströmmar.

Om du vill lägga in annonser i videomaterialet måste du se till att annonsen och det huvudsakliga videomaterialet uppfyller följande krav:

* Annonsinnehållets HLS-version får inte vara högre än huvudinnehållets HLS-version.
* Annonserna måste vara multiplexade och måste innehålla en rendering som bara innehåller ljud, oavsett om huvudinnehållet är multiplexat eller inte.
* Lägg till spellistor bör ha samma bithastighetsåtergivningar som återgivningarna i spellistan för huvudinnehållet.
* Mållängden och den individuella fragmentlängden för en annons får inte överskrida mållängden för huvudinnehållet.
* Om huvudinnehållet innehåller en ström med enbart ljud måste annonsinnehållet även innehålla en ström med enbart ljud.
* Om huvudinnehållet innehåller undertextströmmar måste annonsinnehållet vara okrypterat.
* Om huvudinnehållet är en flerbithastighet (MBR) måste även annonsinnehållet vara MBR.
* Om huvudinnehållet har alternativa ljudspår måste varje annons ha minst en ström med enbart ljud.

   Om annonsen inte har minst en ljudström hoppas annonsen över.