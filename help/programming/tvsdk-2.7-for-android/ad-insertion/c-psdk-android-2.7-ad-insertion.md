---
description: Ni kan infoga annonser i ert VOD-innehåll och direktsänt/linjärt innehåll med hjälp av Adobe Primetime annonsbeslutsgränssnitt.
title: Reklam
exl-id: 79ee4abf-a3f5-4915-ad4b-fe866acec882
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Reklam och dess krav {#advertising-requirements}

Ni kan infoga annonser i ert VOD-innehåll och direktsänt/linjärt innehåll med hjälp av Adobe Primetime annonsbeslutsgränssnitt.

Primetimes annonseringsbeslut fungerar tillsammans med TVSDK för att identifiera annonsmöjligheter, lösa annonser och infoga lösta annonser i era videoströmmar.

Om du vill lägga in annonser i videomaterialet måste du se till att annonsen och det huvudsakliga videomaterialet uppfyller följande krav:

* Annonsinnehållets HLS-version får inte vara högre än huvudinnehållets HLS-version.
* Annonserna behöver inte multiplexas (utan begränsningar), oavsett om huvudinnehållet är multiplexat eller inte.
