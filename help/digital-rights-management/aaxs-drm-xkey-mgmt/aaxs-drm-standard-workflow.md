---
title: Standardarbetsflöde för AXS DRM
description: Standardarbetsflöde för AXS DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
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
