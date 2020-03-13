---
description: För att annonslösaren ska kunna fungera måste annonsleverantörer, som Adobe Primetime och annonsbeslut, ha konfigurationsvärden för att aktivera anslutningen till leverantören.
seo-description: För att annonslösaren ska kunna fungera måste annonsleverantörer, som Adobe Primetime och annonsbeslut, ha konfigurationsvärden för att aktivera anslutningen till leverantören.
seo-title: Lägg in metadata
title: Lägg in metadata
uuid: 8848c939-1f12-4145-8025-453b4fe79aae
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Översikt {#ad-insertion-metadata-overview}

För att annonslösaren ska kunna fungera måste annonsleverantörer, som Adobe Primetime och annonsbeslut, ha konfigurationsvärden för att aktivera anslutningen till leverantören.

Browser TVSDK innehåller Adobe Primetimes annonsbibliotek. För att ditt innehåll ska kunna innehålla annonser från Adobe Primetime-annonsservern måste ditt program tillhandahålla följande obligatoriska AudidtudeSettings-information:

* `mediaID`, som är en unik identifierare för den video som ska spelas upp.

   Utgivaren tilldelar medie-ID när han skickar in videoinnehåll och annonsinformation till Adobe Primetimes annonsbeslutsserver. Detta ID används av Adobe Primetimes annonsbeslut för att hämta relaterad annonsinformation för videon från servern.

* (Valfritt) `defaultMediaId`, som anger vilka annonser som visas när följande villkor uppfylls:

   * Din förfrågan till annonsservern är ogiltig eller så är innehållet felaktigt konfigurerat.
   * Adobe Primetimes annonsbeslut försenas.
   * En av de bakomliggande processerna i Adobe Primetime-annonseringen fungerar inte eller är inte tillgänglig.
   >[!TIP]
   >
   >Adobe rekommenderar att du använder `defaultMediaId`.

* Ditt företag `zoneID`eller din webbplats är tilldelad av Adobe.
* Domänen för den tilldelade annonsservern.
* Andra parametrar för målinriktning.

   Du kan inkludera dessa parametrar beroende på dina behov och annonsleverantörens behov.