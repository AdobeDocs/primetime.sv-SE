---
description: För att annonslösaren ska kunna fungera måste annonsleverantörer, t.ex. Adobe Primetime annonsbeslut, ha konfigurationsvärden för att aktivera anslutningen till leverantören.
title: Lägg till metadata för annonsinfogning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Ökning {#ad-insertion-metadata-overview}

För att annonslösaren ska kunna fungera måste annonsleverantörer, t.ex. Adobe Primetime annonsbeslut, ha konfigurationsvärden för att aktivera anslutningen till leverantören.

Browser TVSDK innehåller Adobe Primetime annonsbeslutsbibliotek. För att ditt innehåll ska innehålla annonser från Adobe Primetime annonsbeslutsserver måste ditt program tillhandahålla följande obligatoriska AudidtudeSettings-information:

* `mediaID`, som är en unik identifierare för den video som ska spelas upp.

  Utgivaren tilldelar medie-ID när han skickar in videoinnehåll och annonsinformation till Adobe Primetime annonsbeslutsserver. Detta ID används av Adobe Primetime annonsbeslut för att hämta relaterad annonsinformation för videon från servern.

* (Valfritt) `defaultMediaId`, som anger vilka annonser som visas när följande villkor uppfylls:

   * Din förfrågan till annonsservern är ogiltig eller så är innehållet felaktigt konfigurerat.
   * Adobe Primetime annonsbeslut försenar spridningen av data.
   * En av Adobe Primetime:s processer för att fatta beslut om bakomliggande annonser fungerar inte eller är inte tillgänglig.

  >[!TIP]
  >
  >Adobe rekommenderar att du använder `defaultMediaId`.

* Dina `zoneID`, som utses av Adobe, identifierar ditt företag eller din webbplats.
* Domänen för den tilldelade annonsservern.
* Andra målparametrar.

  Du kan inkludera dessa parametrar beroende på dina behov och annonsleverantörens behov.
