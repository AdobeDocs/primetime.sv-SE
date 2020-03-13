---
description: Om du vill visa bannerannonser måste du skapa bannerinstanser och tillåta TVSDK att lyssna efter annonsrelaterade händelser.
seo-description: Om du vill visa bannerannonser måste du skapa bannerinstanser och tillåta TVSDK att lyssna efter annonsrelaterade händelser.
seo-title: Visa banners
title: Visa banners
uuid: cfd4b26c-9643-4b60-9aff-bc27dec289f1
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Visa banners {#display-banner-ads}

Om du vill visa bannerannonser måste du skapa bannerinstanser och tillåta TVSDK att lyssna efter annonsrelaterade händelser.

TVSDK tillhandahåller en lista över banners som är kopplade till en linjär annons genom `AdPlaybackEventListener.onAdBreakStart` händelsen.

Manifester kan ange banners för följeslagare genom att:

* Ett HTML-fragment
* URL:en för en iFrame-sida
* URL:en för en statisk bild eller en Adobe Flash SWF-fil

För varje kompletterande annons visar TVSDK vilka typer som är tillgängliga för ditt program.

1. Lägg till en avlyssnare för `AdPlaybackEventListener.onAdBreakStart` händelsen som utför följande:

   * Rensar befintliga annonser i banderollinstansen.
   * Hämtar listan över följeslagarannonser från `Ad.getCompanionAssets`.
   * Om listan med följesedlar inte är tom kan du iterera över listan för banderollinstanser.

      Varje banner-instans (an `AdAsset`) innehåller information, t.ex. bredd, höjd, resurstyp (html, iframe eller static) och data som krävs för att visa den tillhörande bannern.
   * Om en videoannons inte har några följeslagare bokade med sig innehåller listan med följesedlar inga data för den videoannonsen.
   * Om du vill visa en fristående visningsannons lägger du till logiken i skriptet för att köra en vanlig DFP-visningstagg (DoubleClick for Publishers) i rätt banderollinstans.
   * Skickar banderollinformationen till en funktion på sidan som visar banderollerna på lämplig plats.

      Detta är vanligtvis en `div`stil, och funktionen använder `div ID` för att visa banderollen.