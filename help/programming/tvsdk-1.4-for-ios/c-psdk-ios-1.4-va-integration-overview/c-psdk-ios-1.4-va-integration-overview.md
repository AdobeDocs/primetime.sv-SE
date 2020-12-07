---
description: Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.
seo-description: Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.
seo-title: Videoanalys
title: Videoanalys
uuid: 8f297316-f95e-4896-b489-a2d6b36e6b40
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# Integrering av videoanalys {#video-analytics-integration}

Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.

Videospårning i TVSDK använder tjänsten **Adobe Analytics Video Essentials**, som tillhandahåller videointeraktionsstatistik, som videovisningar, färdiga videovisningar, annonsvisningar, hur lång tid som har ägnats åt video och så vidare. Mer information om den här tjänsten får du av Adobe.

Följande procedur sammanfattar stegen som krävs för att aktivera videospårning i spelaren:

1. Initiera och/eller konfigurera följande videospårningskomponenter:

   I iOS är dessa komponenter en del av TVSDK:

   * JSON-konfigurationsfil
   * Metadataobjekt för videoanalys
   * Global metadata-objekt
   * Spårningsobjekt för videoanalys

1. Konfigurera videoanalysrapporter på serversidan med Adobe Analytics Admin Tools.