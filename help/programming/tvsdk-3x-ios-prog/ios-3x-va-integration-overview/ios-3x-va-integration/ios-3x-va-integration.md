---
description: Ni kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.
seo-description: Ni kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.
seo-title: Integrering av videoanalys
title: Integrering av videoanalys
uuid: 275d2c88-a15c-4645-9234-f29d32fc4a63
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Integrering av videoanalys {#video-analytics-integration}

Ni kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.

Videospårning i TVSDK använder tjänsten **Adobe Analytics Video Essentials** , som tillhandahåller videointeraktionsstatistik, som videovisningar, videokompletteringar, annonsvisningar, tidsåtgång för video och så vidare. Kontakta din Adobe-representant om du vill ha mer information om den här tjänsten.

Följande procedur sammanfattar stegen som krävs för att aktivera videospårning i spelaren:

1. Initiera och/eller konfigurera följande videospårningskomponenter:

   I iOS är dessa komponenter en del av TVSDK:

   * JSON-konfigurationsfil
   * Metadataobjekt för videoanalys
   * Global metadata-objekt
   * Spårningsobjekt för videoanalys

1. Konfigurera videoanalysrapporter på serversidan med Adobe Analytics Admin Tools.