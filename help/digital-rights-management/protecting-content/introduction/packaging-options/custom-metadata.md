---
title: Anpassade metadata
description: Anpassade metadata
copied-description: true
exl-id: cfc8b17b-c077-4b28-896d-b1ede1d5090b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Anpassade metadata {#custom-metadata}

Använd det här alternativet om du vill lägga till anpassade nyckel-/värdepar i innehållsmetadata som kan tolkas av serverprogrammet.

Med metadataformatet för Primetimes DRM-innehåll kan du inkludera anpassade nyckel-/värdepar vid paketeringen. Dessa anpassade metadata kan sedan bearbetas av licensservern under licensutfärdandet. Metadata är skilda från en Primetime DRM-princip och kan vara unika för varje innehållsavsnitt.

Exempel: Under en betafas kan du inkludera den anpassade egenskapen `Release:BETA` vid paketeringstid. Licensservrar kan leverera licenser till detta innehåll under betaperioden. När betaperioden har löpt ut tillåter dock licensservrarna inte åtkomst till innehållet.
