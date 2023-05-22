---
title: Out-of-band-licenser
description: Out-of-band-licenser
copied-description: true
exl-id: d9e54c8f-ff82-4834-a62e-20e67c4343dd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Out-of-band-licenser {#out-of-band-licenses}

Med Primetime DRM kan ni implementera ett arbetsflöde där klienter får förgenererade licenser som är out-of-band, och därför slipper ni driftsätta en licensserver. För att stödja det här arbetsflödet bör ett alternativ som anger att ingen licensserver är tillgänglig anges vid paketeringen. Detta förhindrar klienten från att försöka begära en licens för det här innehållet från en licensserver.

Innehåll som anger att en licensserver inte är tillgänglig kan bara spelas upp på Primetimes DRM-klienter version 3.0 eller senare. Äldre kunder måste uppgradera för att kunna spela upp det här innehållet.
