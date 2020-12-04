---
seo-title: Standardarbetsflöde för AXS DRM
title: Standardarbetsflöde för AXS DRM
description: Standardarbetsflöde för AXS DRM
seo-description: Standardarbetsflöde för AXS DRM
uuid: b996eb2c-8e37-4a29-a972-e09c69d2461d
translation-type: tm+mt
source-git-commit: 17a492d30c65b1b5e12419f04afa0116654b99fc
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Standard AXS DRM-arbetsflöde{#standard-aaxs-drm-workflow}

1. (Paket) AAXS Java SDK genererar en slumpmässig CEK.
1. (Paket) CEK används för att kryptera innehåll.
1. (Paket) CEK krypteras med AXS-licensserverns offentliga nyckel.
1. (Paket) Den krypterade CK infogas i innehållets DRM-metadata.
1. Enheten försöker spela upp innehåll genom att begära en licens från AXS-servern.
1. (Licensiering) AAXS-servern använder sin privata nyckel för att dekryptera CEK från metadata.
1. (Licensiering) AAXS-servern utfärdar en licens som innehåller CEK till enheten.
