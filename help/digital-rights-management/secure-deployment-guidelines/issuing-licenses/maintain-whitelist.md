---
description: En vitlista är en lista över betrodda enheter.
seo-description: En vitlista är en lista över betrodda enheter.
seo-title: Underhåll en vitlista över pålitliga innehållspaket
title: Underhåll en vitlista över pålitliga innehållspaket
uuid: 9a132ef9-eb56-408a-939e-1acd32d83a33
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Underhåll en vitlista över pålitliga innehållspaket{#maintain-a-whitelist-of-trusted-content-packagers}

En vitlista är en lista över betrodda enheter.

För innehållspaket är enheterna organisationer som av innehållsägaren är betrodda att paketera (eller kryptera) videofilerna och skapa DRM-skyddat innehåll. När du distribuerar Adobe Primetime DRM bör du ha en vitlista över betrodda innehållspaket. Du måste också verifiera identiteten på innehållspaketeraren i DRM-metadata för en DRM-skyddad fil innan du kan utfärda en licens.

Mer information om hur du hämtar information om enheten som paketerade innehållet finns i [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).
