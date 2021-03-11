---
description: Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.
title: Videoanalys
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Videoanalys{#video-analytics}

Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.

Videospårning i TVSDK använder tjänsten **Adobe Analytics Video Essentials**, som tillhandahåller videointeraktionsstatistik, som videovisningar, färdiga videovisningar, annonsvisningar, hur lång tid som har ägnats åt video och så vidare. Mer information om den här tjänsten får du av Adobe.

Följande procedur sammanfattar stegen som krävs för att aktivera videospårning i spelaren:

1. Initiera och/eller konfigurera följande videospårningskomponenter:

   På Android är dessa komponenter en del av TVSDK:

   * JSON-konfigurationsfil
   * Metadataobjekt för videoanalys
   * Global metadata-objekt

1. Konfigurera videoanalysrapporter på serversidan med Adobe Analytics Admin Tools.

