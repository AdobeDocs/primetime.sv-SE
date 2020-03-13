---
seo-title: Underhåll en vitlista över pålitliga innehållspaket
title: Underhåll en vitlista över pålitliga innehållspaket
uuid: ad40993c-15c3-43b2-9593-7b75802cfe69
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Underhåll en vitlista över pålitliga innehållspaket{#maintain-a-whitelist-of-trusted-content-packagers}

En *vitlista* är en lista över betrodda enheter. När det gäller innehållspaket är det organisationer som ägaren av innehållet litar på för att paketera (eller kryptera) FLV-/F4V-videofiler och skapa DRM-skyddat innehåll. När du distribuerar Adobe Access rekommenderar vi att du upprätthåller en vitlista över betrodda innehållspaket och att du kontrollerar identiteten för innehållspaketeraren som finns i DRM-metadata (DRM-huvudet) för en DRM-skyddad fil innan du utfärdar en licens.

Mer information om hur du hämtar information om enheten som paketerade innehållet finns `V2ContentMetaData.getPackagerInfo()` i API-referens *för* Adobe Access.
