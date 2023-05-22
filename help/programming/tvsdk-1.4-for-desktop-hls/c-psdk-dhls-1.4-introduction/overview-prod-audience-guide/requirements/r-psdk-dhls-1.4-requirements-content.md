---
description: Kontrollera begränsningar och krav för strömmar och spellistor (manifest), inklusive DRM-krypteringsnycklar.
title: Krav för innehåll och manifest
exl-id: 96b2b245-558b-4606-87c0-22140430c326
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
