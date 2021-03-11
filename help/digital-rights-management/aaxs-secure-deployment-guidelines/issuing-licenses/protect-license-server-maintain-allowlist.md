---
title: Underhåll en tillåtelselista av pålitliga innehållspaket
description: Underhåll en tillåtelselista av pålitliga innehållspaket
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Underhåll en tillåtelselista med betrodda innehållspaket {#maintain-a-allowlist-of-trusted-content-packagers}

En **tillåtelselista** är en lista över betrodda enheter. När det gäller innehållspaket är det organisationer som ägaren av innehållet litar på för att paketera (eller kryptera) FLV-/F4V-videofiler och skapa DRM-skyddat innehåll. När du distribuerar Adobe Access rekommenderar vi att du upprätthåller en tillåtelselista med betrodda innehållspaket och att du kontrollerar identiteten för innehållspaketeraren som finns i DRM-metadata (DRM-huvudet) för en DRM-skyddad fil innan du utfärdar en licens.

Mer information om hur du hämtar information om enheten som paketerade innehållet finns i `V2ContentMetaData.getPackagerInfo()` i *API-referens för Adobe Access*.
