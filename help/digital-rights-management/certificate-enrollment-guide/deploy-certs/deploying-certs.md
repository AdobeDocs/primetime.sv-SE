---
seo-title: Distribuera certifikat
title: Distribuera certifikat
uuid: adf72b51-be0f-49ec-83f7-152a378b04e6
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# Distribuera certifikat{#deploy-certificates}

För att undvika att PFX-lösenordet är tillgängligt i klartext på licensservern kräver referensimplementeringen och Adobe Primetime DRM Server for Protected Streaming att lösenordet krypteras när det anges i konfigurationsfilen. Se *Använda implementeringar av DRM-referens för Primetime* eller *Använda DRM-servern* för skyddad direktuppspelning för instruktioner om hur du kör förvrängningsverktygen. Var och en av dem har ett eget krypteringsverktyg och de krypterade lösenorden är inte utbytbara mellan dessa två implementeringar av licensservern.

Information om hur du distribuerar certifikat och förvrängda lösenord till licensservern finns i *Använda implementeringar av DRM-referens för Primetime* eller *Använda DRM-servern för skyddad direktuppspelning*.
