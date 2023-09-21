---
title: Underhåll en tillåtelselista av pålitliga innehållspaket
description: Underhåll en tillåtelselista av pålitliga innehållspaket
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# Underhåll en tillåtelselista av pålitliga innehållspaket {#maintain-a-allowlist-of-trusted-content-packagers}

An **tillåtelselista** är en lista över betrodda enheter. När det gäller innehållspaket är det organisationer som ägaren av innehållet litar på för att paketera (eller kryptera) FLV-/F4V-videofiler och skapa DRM-skyddat innehåll. När du distribuerar Adobe Access rekommenderar vi att du upprätthåller en tillåtelselista med betrodda innehållspaket och att du kontrollerar identiteten för innehållspaketeraren som finns i DRM-metadata (DRM-huvudet) för en DRM-skyddad fil innan du utfärdar en licens.

Mer information om hur du hämtar information om enheten som paketerade innehållet finns i `V2ContentMetaData.getPackagerInfo()` i *API-referens för Adobe Access*.
