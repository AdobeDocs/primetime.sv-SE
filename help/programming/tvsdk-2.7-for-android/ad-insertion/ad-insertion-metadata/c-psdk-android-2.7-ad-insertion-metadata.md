---
description: För att annonslösaren ska kunna fungera måste annonsleverantörer, som Adobe Primetime och annonsbeslut, ha konfigurationsvärden för att aktivera anslutningen till leverantören.
seo-description: För att annonslösaren ska kunna fungera måste annonsleverantörer, som Adobe Primetime och annonsbeslut, ha konfigurationsvärden för att aktivera anslutningen till leverantören.
seo-title: Lägg in metadata
title: Lägg in metadata
uuid: ee4dd8b8-4c41-4f01-be50-60f4c7dc962d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Översikt {#ad-insertion-metadata-overview}

För att annonslösaren ska kunna fungera måste annonsleverantörer, som Adobe Primetime och annonsbeslut, ha konfigurationsvärden för att aktivera anslutningen till leverantören.

TVSDK innehåller annonseringsbiblioteket Primetime. För att ditt innehåll ska innehålla annonser från Primetimes annonsserver måste ditt program tillhandahålla följande obligatoriska `AuditudeSettings` information:

* `mediaID`, som är en unik identifierare för den video som ska spelas upp.

   Utgivaren tilldelar medie-ID när han skickar in videoinnehåll och annonsinformation till Adobe Primetimes annonsbeslutsserver. Detta ID används av Primetimes annonsbeslut för att hämta relaterad annonsinformation för videon från servern.

* (Valfritt) `defaultMediaId`, som anger vilka annonser som visas när följande villkor uppfylls:

   * Din förfrågan till annonsservern är ogiltig eller så är innehållet felaktigt konfigurerat.
   * Primetimes annonsbeslut försenar spridningen av data.
   * En av de bakomliggande processerna för annonsering i Primetime är felfungerande eller inte tillgänglig.
   >[!TIP]
   >
   >Adobe rekommenderar att du använder `defaultMediaId`.

* Ditt företag `zoneID`eller din webbplats är tilldelad av Adobe.
* Domänen för den tilldelade annonsservern.
* Andra parametrar för målinriktning.

   Du kan inkludera dessa parametrar beroende på dina behov och annonsleverantörens behov.