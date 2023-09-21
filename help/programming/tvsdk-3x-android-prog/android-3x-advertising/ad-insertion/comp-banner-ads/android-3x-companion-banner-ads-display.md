---
description: Om du vill visa bannerannonser måste du skapa bannerinstanser och tillåta TVSDK att lyssna efter annonsrelaterade händelser.
title: Visa banners
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Visa banners {#display-banner-ads}

Om du vill visa bannerannonser måste du skapa bannerinstanser och tillåta TVSDK att lyssna efter annonsrelaterade händelser.

TVSDK tillhandahåller en lista över bannerannonser som är kopplade till en linjär annons via `AdPlaybackEventListener.onAdBreakStart` -händelse.

Manifester kan ange banners för följeslagare genom att:

* Ett HTML-fragment
* URL:en för en iFrame-sida
* URL:en för en statisk bild eller en SWF-fil i Adobe Flash

För varje kompletterande annons visar TVSDK vilka typer som är tillgängliga för ditt program.

1. Lägg till en avlyssnare för `AdPlaybackEventListener.onAdBreakStart` händelse som gör följande:

   * Rensar befintliga annonser i banderollinstansen.
   * Hämtar listan över annonser från `Ad.getCompanionAssets`.
   * Om listan med följesedlar inte är tom kan du iterera över listan för banderollinstanser.

     Varje banner-instans (en `AdAsset`) innehåller information som bredd, höjd, resurstyp (html, iframe eller static) och data som krävs för att visa den tillhörande banderollen.
   * Om en videoannons inte har några följeslagare bokade med sig innehåller listan med följesedlar inga data för den videoannonsen.
   * Om du vill visa en fristående visningsannons lägger du till logiken i skriptet för att köra en vanlig DFP-visningstagg (DoubleClick for Publishers) i rätt banderollinstans.
   * Skickar banderollinformationen till en funktion på sidan som visar banderollerna på lämplig plats.

     Detta är vanligtvis en `div`och funktionen använder `div ID` för att visa banderollen.
