---
description: En lista över tillåtna är en lista över betrodda enheter.
seo-description: En lista över tillåtna är en lista över betrodda enheter.
seo-title: Underhåll en lista över tillåtna paket med betrott innehåll
title: Underhåll en lista över tillåtna paket med betrott innehåll
uuid: 9a132ef9-eb56-408a-939e-1acd32d83a33
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---


# Underhåll en lista över betrodda innehållspaket{#maintain-a-allowlist-of-trusted-content-packagers}

En lista över tillåtna är en lista över betrodda enheter.

För innehållspaket är enheterna organisationer som av innehållsägaren är betrodda att paketera (eller kryptera) videofilerna och skapa DRM-skyddat innehåll. När du distribuerar Adobe Primetime DRM bör du ha en lista över betrodda innehållspaket som kan användas. Du måste också verifiera identiteten på innehållspaketeraren i DRM-metadata för en DRM-skyddad fil innan du kan utfärda en licens.

Mer information om hur du hämtar information om enheten som paketerade innehållet finns i [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).
