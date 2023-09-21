---
description: Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.
title: Videoanalys
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Ökning {#video-analytics-overview}

Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.

Videospårning i TVSDK använder **Adobe Analytics Video Essentials** som tillhandahåller interaktionsstatistik för video, som videovisningar, kompletta videofilmer, annonsvisningar, tidsåtgång för video och så vidare. Mer information om den här tjänsten får du av Adobe.

Följande procedur sammanfattar stegen som krävs för att aktivera videospårning i spelaren:

1. Initiera och/eller konfigurera följande videospårningskomponenter:

   >[!TIP]
   >
   >I Android är de här komponenterna en del av TVSDK.

   * JSON-konfigurationsfil
   * Metadataobjekt för videoanalys
   * Global metadata-objekt

1. Konfigurera videoanalysrapporter på serversidan med Adobe Analytics Admin Tools.
