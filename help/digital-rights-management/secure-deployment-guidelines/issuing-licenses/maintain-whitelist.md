---
description: En tillåtelselista är en lista över betrodda enheter.
seo-description: En tillåtelselista är en lista över betrodda enheter.
seo-title: Underhåll en tillåtelselista av pålitliga innehållspaket
title: Underhåll en tillåtelselista av pålitliga innehållspaket
uuid: 9a132ef9-eb56-408a-939e-1acd32d83a33
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Underhåll en tillåtelselista med betrodda innehållspaket {#maintain-a-allowlist-of-trusted-content-packagers}

En tillåtelselista är en lista över betrodda enheter.

För innehållspaket är enheterna organisationer som av innehållsägaren är betrodda att paketera (eller kryptera) videofilerna och skapa DRM-skyddat innehåll. När du distribuerar Adobe Primetime DRM bör du ha en tillåtelselista med betrodda innehållspaket. Du måste också verifiera identiteten på innehållspaketeraren i DRM-metadata för en DRM-skyddad fil innan du kan utfärda en licens.

Mer information om hur du får information om enheten som paketerade innehållet finns i [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).
