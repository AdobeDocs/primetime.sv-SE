---
seo-title: Out-of-band-licenser
title: Out-of-band-licenser
uuid: 43397ce5-6c52-429d-b7fa-fa8c91cf9742
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Out-of-band-licenser {#out-of-band-licenses}

Med Primetime DRM kan ni implementera ett arbetsflöde där klienter får förgenererade licenser som är out-of-band, och därför slipper ni driftsätta en licensserver. För att stödja det här arbetsflödet bör ett alternativ som anger att ingen licensserver är tillgänglig anges vid paketeringen. Detta förhindrar klienten från att försöka begära en licens för det här innehållet från en licensserver.

Innehåll som anger att en licensserver inte är tillgänglig kan bara spelas upp på Primetimes DRM-klienter version 3.0 eller senare. Äldre kunder måste uppgradera för att kunna spela upp det här innehållet.
