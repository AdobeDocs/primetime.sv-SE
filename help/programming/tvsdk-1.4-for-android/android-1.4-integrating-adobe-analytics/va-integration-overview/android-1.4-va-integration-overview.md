---
description: Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.
seo-description: Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.
seo-title: Videoanalys
title: Videoanalys
uuid: 4cb589fd-7b29-4f43-870d-17430ff309f7
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '135'
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

