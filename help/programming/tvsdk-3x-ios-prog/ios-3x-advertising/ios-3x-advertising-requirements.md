---
description: Ni kan infoga annonser i ert VOD-innehåll och direktsänt/linjärt innehåll med hjälp av Adobe Primetime annonsbeslutsgränssnitt.
title: Krav för annonsering
translation-type: tm+mt
source-git-commit: 944bfb0f3bd0050a9d2974a37f4fabddaaac8a93
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---


# Krav för annonsering {#advertising-requirements}

Ni kan infoga annonser i ert VOD-innehåll och direktsänt/linjärt innehåll med hjälp av Adobe Primetime annonsbeslutsgränssnitt.

<!--<a id="section_A2966DC850E140FE9400A1D9E412F819"></a>-->

Primetimes annonsbeslut fungerar tillsammans med TVSDK för att identifiera annonsmöjligheter, lösa annonser och infoga lösta annonser i era videoströmmar.

Om du vill lägga in annonser i videomaterialet måste du se till att annonsen och det huvudsakliga videomaterialet uppfyller följande krav:

* Annonsinnehållets HLS-version får inte vara högre än huvudinnehållets HLS-version.
* Annonserna måste vara multiplexade och måste innehålla en rendering som bara innehåller ljud, oavsett om huvudinnehållet är multiplexat eller inte.
* Lägg till spellistor bör ha samma bithastighetsåtergivningar som återgivningarna i spellistan för huvudinnehållet.
* Mållängden och den individuella fragmentlängden för en annons får inte överskrida mållängden för huvudinnehållet.
* Om huvudinnehållet innehåller en ström med enbart ljud måste annonsinnehållet även innehålla en ström med enbart ljud.
* Om huvudinnehållet innehåller undertextströmmar måste annonsinnehållet vara okrypterat.
* Om huvudinnehållet är en flerbithastighet (MBR) måste även annonsinnehållet vara MBR.
* Om huvudinnehållet har alternativa ljudspår måste varje annons ha minst en ström med enbart ljud, annars ska annonserna demultiplexas. Om annonsen varken har minst en ström med enbart ljud eller är demuxerad hoppas annonsen över.