---
seo-title: Anpassade metadata
title: Anpassade metadata
uuid: 99bdef62-32a9-4fd0-919c-5a2594e8d17e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Anpassade metadata {#custom-metadata}

Använd det här alternativet om du vill lägga till anpassade nyckel-/värdepar i innehållsmetadata som kan tolkas av serverprogrammet.

Med metadataformatet för Primetimes DRM-innehåll kan du inkludera anpassade nyckel-/värdepar vid paketeringen. Dessa anpassade metadata kan sedan bearbetas av licensservern under licensutfärdandet. Metadata är skilda från en Primetime DRM-princip och kan vara unika för varje innehållsavsnitt.

Exempel: Under en betafas kan du inkludera den anpassade egenskapen `Release:BETA` vid paketeringen. Licensservrar kan leverera licenser till detta innehåll under betaperioden. När betaperioden har löpt ut tillåter dock licensservrarna inte åtkomst till innehållet.
