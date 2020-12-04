---
description: Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.
seo-description: Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.
seo-title: Integrera TVSDK med Adobe Analytics
title: Integrera TVSDK med Adobe Analytics
uuid: 4d498d35-ec8e-40fc-8272-1637ef942bb0
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Integrera TVSDK med Adobe Analytics {#integrating-tvsdk-with-adobe-analytics}

Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.

Videospårning i TVSDK använder tjänsten **Adobe Analytics Video Essentials**, som tillhandahåller videointeraktionsstatistik, som videovisningar, färdiga videovisningar, annonsvisningar, hur lång tid som har ägnats åt video och så vidare. Mer information om den här tjänsten får du av Adobe.

Följande procedur sammanfattar stegen som krävs för att aktivera videospårning i spelaren:

1. Initiera och/eller konfigurera följande videospårningskomponenter:

   >[!TIP]
   >
   >I Android är de här komponenterna en del av TVSDK.

   * JSON-konfigurationsfil
   * Metadataobjekt för videoanalys
   * Global metadata-objekt

1. Konfigurera videoanalysrapporter på serversidan med Adobe Analytics Admin Tools.