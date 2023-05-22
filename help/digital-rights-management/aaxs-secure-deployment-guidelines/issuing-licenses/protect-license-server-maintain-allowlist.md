---
title: Underhåll en tillåtelselista av pålitliga innehållspaket
description: Underhåll en tillåtelselista av pålitliga innehållspaket
copied-description: true
exl-id: 4c296d23-75c1-4d0b-a636-31b49e99c753
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# Underhåll en tillåtelselista av pålitliga innehållspaket {#maintain-a-allowlist-of-trusted-content-packagers}

An **tillåtelselista** är en lista över betrodda enheter. När det gäller innehållspaket är det organisationer som ägaren av innehållet litar på för att paketera (eller kryptera) FLV-/F4V-videofiler och skapa DRM-skyddat innehåll. När du distribuerar Adobe Access rekommenderar vi att du upprätthåller en tillåtelselista med betrodda innehållspaket och att du kontrollerar identiteten för innehållspaketeraren som finns i DRM-metadata (DRM-huvudet) för en DRM-skyddad fil innan du utfärdar en licens.

Mer information om hur du hämtar information om enheten som paketerade innehållet finns i `V2ContentMetaData.getPackagerInfo()` i *API-referens för Adobe Access*.
