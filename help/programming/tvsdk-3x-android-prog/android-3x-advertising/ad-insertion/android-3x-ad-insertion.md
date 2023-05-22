---
description: Ni kan infoga annonser i ert VOD-innehåll och direktsänt/linjärt innehåll med hjälp av Adobe Primetime annonsbeslutsgränssnitt. Primetimes annonseringsbeslut fungerar tillsammans med TVSDK för att identifiera annonsmöjligheter, lösa annonser och infoga lösta annonser i era videoströmmar.
title: Krav för annonsering
exl-id: 3ca82cc5-ed64-458e-9a8d-475a84512478
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Reklam och dess krav {#advertising-requirements}

Ni kan infoga annonser i ert VOD-innehåll och direktsänt/linjärt innehåll med hjälp av Adobe Primetime annonsbeslutsgränssnitt. Primetimes annonseringsbeslut fungerar tillsammans med TVSDK för att identifiera annonsmöjligheter, lösa annonser och infoga lösta annonser i era videoströmmar.

<!--<a id="section_282A8000A8BF4860A24F0D3F1A19BC9E"></a>-->

Om du vill lägga in annonser i videomaterialet måste du se till att annonsen och det huvudsakliga videomaterialet uppfyller följande krav:

* Annonsinnehållets HLS-version får inte vara högre än huvudinnehållets HLS-version.
* Annonserna behöver inte multiplexas (utan begränsningar), oavsett om huvudinnehållet är multiplexat eller inte.
