---
title: Distribuera certifikat
description: Distribuera certifikat
copied-description: true
exl-id: 649c4f24-f74e-4529-84a2-65bcd6d7677c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# Distribuera certifikat{#deploy-certificates}

För att undvika att PFX-lösenordet är tillgängligt i klartext på licensservern kräver referensimplementeringen och Adobe Primetime DRM Server for Protected Streaming att lösenordet krypteras när det anges i konfigurationsfilen. Se *Använda implementeringar av DRM-referenser för Primetime* eller *Använda Primetime DRM-servern* för Skyddad strömning för instruktioner om hur du kör förvrängningsverktygen. Var och en av dem har ett eget krypteringsverktyg och de krypterade lösenorden är inte utbytbara mellan dessa två implementeringar av licensservern.

Information om hur du distribuerar certifikat och lösenord till licensservern finns i *Använda implementeringar av DRM-referenser för Primetime* eller *Använda Primetime DRM-servern för skyddad strömning*.
