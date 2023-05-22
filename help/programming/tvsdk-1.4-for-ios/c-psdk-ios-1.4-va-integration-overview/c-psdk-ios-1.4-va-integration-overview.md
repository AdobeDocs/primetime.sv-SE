---
description: Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.
title: Videoanalys
exl-id: 8999ce57-681b-44f1-b337-3216b3883ad9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '127'
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
