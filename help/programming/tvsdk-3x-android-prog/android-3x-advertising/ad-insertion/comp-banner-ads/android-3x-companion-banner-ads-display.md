---
description: Om du vill visa bannerannonser måste du skapa bannerinstanser och tillåta TVSDK att lyssna efter annonsrelaterade händelser.
title: Visa banners
exl-id: 3ccf6525-ffc1-4f45-a662-8b53cab0f448
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
* URL-adressen till en statisk bild eller en Adobe Flash SWF-fil

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
