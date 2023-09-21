---
title: Standardarbetsflöde för AXS DRM
description: Standardarbetsflöde för AXS DRM
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# Standardarbetsflöde för AXS DRM{#standard-aaxs-drm-workflow}

1. (Paket) AAXS Java SDK genererar en slumpmässig CEK.
1. (Paket) CEK används för att kryptera innehåll.
1. (Paket) CEK krypteras med AXS-licensserverns offentliga nyckel.
1. (Paket) Den krypterade CK infogas i innehållets DRM-metadata.
1. Enheten försöker spela upp innehåll genom att begära en licens från AXS-servern.
1. (Licensiering) AAXS-servern använder sin privata nyckel för att dekryptera CEK från metadata.
1. (Licensiering) AAXS-servern utfärdar en licens som innehåller CEK till enheten.
