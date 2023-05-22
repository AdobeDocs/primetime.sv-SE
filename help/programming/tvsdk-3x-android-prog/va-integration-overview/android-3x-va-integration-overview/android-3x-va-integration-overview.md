---
description: Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.
title: Integrera TVSDK med Adobe Analytics
exl-id: d6e235ad-dffb-4503-bf6f-f7a780523791
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# Integrera TVSDK med Adobe Analytics {#integrating-tvsdk-with-adobe-analytics}

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
