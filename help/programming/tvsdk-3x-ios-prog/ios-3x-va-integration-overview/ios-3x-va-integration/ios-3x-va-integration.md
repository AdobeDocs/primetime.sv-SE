---
description: Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.
title: Integrering av videoanalys
exl-id: c335b864-7468-49ae-ab7f-0d23f3d5bc25
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# Integrering av videoanalys {#video-analytics-integration}

Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.

Videospårning i TVSDK använder **Adobe Analytics Video Essentials** som tillhandahåller interaktionsstatistik för video, som videovisningar, kompletta videofilmer, annonsvisningar, tidsåtgång för video och så vidare. Mer information om den här tjänsten får du av Adobe.

Följande procedur sammanfattar stegen som krävs för att aktivera videospårning i spelaren:

1. Initiera och/eller konfigurera följande videospårningskomponenter:

   I iOS ingår följande komponenter i TVSDK:

   * JSON-konfigurationsfil
   * Metadataobjekt för videoanalys
   * Global metadata-objekt
   * Spårningsobjekt för videoanalys

1. Konfigurera videoanalysrapporter på serversidan med Adobe Analytics Admin Tools.
