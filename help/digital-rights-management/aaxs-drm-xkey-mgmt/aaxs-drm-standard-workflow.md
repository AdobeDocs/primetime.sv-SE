---
title: Standardarbetsflöde för AXS DRM
description: Standardarbetsflöde för AXS DRM
exl-id: 3bc6aa6a-cda6-4c83-af08-f27eb103a47a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
