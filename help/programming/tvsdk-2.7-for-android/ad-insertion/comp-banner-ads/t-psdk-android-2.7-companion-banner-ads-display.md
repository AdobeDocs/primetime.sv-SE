---
description: Om du vill visa bannerannonser måste du skapa bannerinstanser och tillåta TVSDK att lyssna efter annonsrelaterade händelser.
seo-description: Om du vill visa bannerannonser måste du skapa bannerinstanser och tillåta TVSDK att lyssna efter annonsrelaterade händelser.
seo-title: Visa banners
title: Visa banners
uuid: 7246dfab-860f-4b55-9554-49738a483406
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# Visa banners {#display-banner-ads}

Om du vill visa bannerannonser måste du skapa bannerinstanser och tillåta TVSDK att lyssna efter annonsrelaterade händelser.

TVSDK innehåller en lista med bannerannonser som är kopplade till en linjär annons via händelsen `AdPlaybackEventListener.onAdBreakStart`.

Manifester kan ange banners för följeslagare genom att:

* Ett HTML-fragment
* URL:en för en iFrame-sida
* URL:en för en statisk bild eller en SWF-fil i Adobe Flash

För varje kompletterande annons visar TVSDK vilka typer som är tillgängliga för ditt program.

1. Lägg till en avlyssnare för händelsen `AdPlaybackEventListener.onAdBreakStart` som gör följande:

   * Rensar befintliga annonser i banderollinstansen.
   * Hämtar listan över följeslagarannonser från `Ad.getCompanionAssets`.
   * Om listan med följesedlar inte är tom kan du iterera över listan för banderollinstanser.

      Varje banderollinstans (en `AdAsset`) innehåller information som bredd, höjd, resurstyp (html, iframe eller static) och data som krävs för att visa den tillhörande banderollen.
   * Om en videoannons inte har några följeslagare bokade med sig innehåller listan med följesedlar inga data för den videoannonsen.
   * Om du vill visa en fristående visningsannons lägger du till logiken i skriptet för att köra en vanlig DFP-visningstagg (DoubleClick for Publishers) i rätt banderollinstans.
   * Skickar banderollinformationen till en funktion på sidan som visar banderollerna på lämplig plats.

      Det här är vanligtvis en `div` och funktionen använder `div ID` för att visa banderollen.

