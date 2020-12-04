---
description: Kontrollera begränsningar och krav för strömmar och spellistor (manifest), inklusive DRM-krypteringsnycklar.
seo-description: Kontrollera begränsningar och krav för strömmar och spellistor (manifest), inklusive DRM-krypteringsnycklar.
seo-title: Krav för innehåll och manifest
title: Krav för innehåll och manifest
uuid: 53cc570a-be33-4488-95e8-43f91b559b13
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---


# Krav för innehåll och manifest {#content-and-manifest-requirements}

Kontrollera begränsningar och krav för strömmar och spellistor (manifest), inklusive DRM-krypteringsnycklar.

| Inkludera och ange egenskapen `RESOLUTION` för varje ABR-ström i manifestfilen. Du måste använda Flash Player 14 eller senare. |
|---|
| Om den DRM-skyddade strömmen har flera bithastigheter (MBR) bör DRM-krypteringsnyckeln som används för MBR vara densamma som nyckeln som används i alla bithastighetsströmmar. |
| Måste ha samma bithastighetsåtergivningar som återgivningarna av huvudinnehållet. |