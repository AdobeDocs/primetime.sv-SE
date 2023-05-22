---
title: Förutsättningar
description: Förutsättningar
copied-description: true
exl-id: 1b66f7fd-ea2f-4217-b327-910e90ab889d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Förutsättningar {#prerequisites}

Innan du paketerar innehåll krävs ett Primetime DRM Packager-certifikat. Det måste begäras via registreringsprocessen för DRM-certifikat från Primetime. Endast ett paketerarcertifikat krävs (ingen licensserver eller transport). Ange i e-postmeddelandet om certifikatbegäran att begäran avser ett certifikat som ska användas med DRM-tjänsten.

[Handbok för registrering av certifikat](../../digital-rights-management/certificate-enrollment-guide/about-certs.md)

Det finns två nivåer av förpackningscertifikat - PRODUKTION och TESTVERSION. Innehåll som paketeras med TRIAL-certifikat är endast avsett för utveckling och kommer inte att spelas upp när certifikatet har upphört att gälla. Alla licenser som utfärdas för TRIAL-innehåll har ett maximalt förfallodatum för en hårdkodad princip som är lika med utgångsdatumet för certifikatet (om det inte anges i DRM-principen).
