---
description: En tillåtelselista är en lista över betrodda enheter.
title: Underhåll en tillåtelselista av pålitliga innehållspaket
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Underhåll en tillåtelselista med betrodda innehållspaket {#maintain-a-allowlist-of-trusted-content-packagers}

En tillåtelselista är en lista över betrodda enheter.

För innehållspaket är enheterna organisationer som av innehållsägaren är betrodda att paketera (eller kryptera) videofilerna och skapa DRM-skyddat innehåll. När du distribuerar Adobe Primetime DRM bör du ha en tillåtelselista med betrodda innehållspaket. Du måste också verifiera identiteten på innehållspaketeraren i DRM-metadata för en DRM-skyddad fil innan du kan utfärda en licens.

Mer information om hur du får information om enheten som paketerade innehållet finns i [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).
