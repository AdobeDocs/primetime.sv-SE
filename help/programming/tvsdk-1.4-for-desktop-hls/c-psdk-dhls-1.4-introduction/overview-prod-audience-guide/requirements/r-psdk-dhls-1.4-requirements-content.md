---
description: Kontrollera begränsningar och krav för strömmar och spellistor (manifest), inklusive DRM-krypteringsnycklar.
title: Krav för innehåll och manifest
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---


# Krav för innehåll och manifest {#content-and-manifest-requirements}

Kontrollera begränsningar och krav för strömmar och spellistor (manifest), inklusive DRM-krypteringsnycklar.

| Inkludera och ange egenskapen `RESOLUTION` för varje ABR-ström i manifestfilen. Du måste använda Flash Player 14 eller senare. |
|---|
| Om den DRM-skyddade strömmen har flera bithastigheter (MBR) bör DRM-krypteringsnyckeln som används för MBR vara densamma som nyckeln som används i alla bithastighetsströmmar. |
| Måste ha samma bithastighetsåtergivningar som återgivningarna av huvudinnehållet. |