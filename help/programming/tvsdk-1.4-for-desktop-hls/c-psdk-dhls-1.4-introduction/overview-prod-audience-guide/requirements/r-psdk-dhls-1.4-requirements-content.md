---
description: Kontrollera begränsningar och krav för strömmar och spellistor (manifest), inklusive DRM-krypteringsnycklar.
title: Krav för innehåll och manifest
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Krav för innehåll och manifest {#content-and-manifest-requirements}

Kontrollera begränsningar och krav för strömmar och spellistor (manifest), inklusive DRM-krypteringsnycklar.

| Inkludera och ange `RESOLUTION` för varje ABR-ström i manifestfilen. Du måste använda Flash Player 14 eller senare. |
|---|
| Om den DRM-skyddade strömmen har flera bithastigheter (MBR) bör DRM-krypteringsnyckeln som används för MBR vara densamma som nyckeln som används i alla bithastighetsströmmar. |
| Måste ha samma bithastighetsåtergivningar som återgivningarna av huvudinnehållet. |
