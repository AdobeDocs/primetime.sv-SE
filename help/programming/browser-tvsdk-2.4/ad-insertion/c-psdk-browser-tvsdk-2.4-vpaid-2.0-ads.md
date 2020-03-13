---
description: VPAID 2.0 (Video Player ad-sting interface definition) ger ett gemensamt gränssnitt för att spela upp videoannonser. Det ger en multimedieupplevelse för användarna och gör det möjligt för utgivare att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll.
seo-description: VPAID 2.0 (Video Player ad-sting interface definition) ger ett gemensamt gränssnitt för att spela upp videoannonser. Det ger en multimedieupplevelse för användarna och gör det möjligt för utgivare att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll.
seo-title: Stöd för VPAID 2.0
title: Stöd för VPAID 2.0
uuid: 462692b5-c4b3-4488-adb3-f309809d64ad
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Stöd för VPAID 2.0 {#vpaid-ad-support}

VPAID 2.0 (Video Player ad-sting interface definition) ger ett gemensamt gränssnitt för att spela upp videoannonser. Det ger en multimedieupplevelse för användarna och gör det möjligt för utgivare att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll.

Följande funktioner stöds:

* Version 2.0 av VPAID-specifikationen

   Mer information finns i [IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/).
* Linjära VPAID-annonser med VOD-innehåll (video on demand)
* I Live-innehåll har Browser TVSDK stöd för JavaScript VPAID-annonser före användning.
* I Flash grundläge stöder Browser TVSDK bara Flash-baserade VPAID-annonser.
* Linjära JavaScript VPAID-annonser

   VPAID-annonser måste vara JavaScript-baserade, och annonssvaret måste identifiera medietypen för VPAID-annonsen som `application/javascript`.

Följande funktioner stöds inte:

* Version 1.0 av VPAID-specifikationen
* Överhoppade annonser
* Annonser som inte finns online, som överläggsannonser, dynamiska följeslagarannonser, minimeringsbara annonser, komprimerbara annonser och expanderbara annonser.
* Förhandsladda VPAID-annonser
* VPAID-annonser i direktinnehåll
* Flash VPAID-annonser

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

Följande API-element stöder VPAID 2.0-annonser:

* Metoden `getCustomAdView` för `MediaPlayer` returnerar ett `CustomAdView` objekt, som representerar webbvyn som återger VPAID-annonsen.

   Mer information om `getCustomAdView` metoden finns i [dokumentationen](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html)för MediaPlayer API.

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` anger timeout för VPAID-inläsningsprocessen.

   Standardvärdet för timeout är 10 sekunder.

* Med API:t `auditudeSettings.ignoreVPAIDAds`kan du ignorera VPAID-annonser som tagits emot från Auditude-servern. API:t fungerar inte för Flash Fallback.

Under uppspelningen av VPAID-annonsen:

* VPAID-annonsen visas i en visningsbehållare ovanför spelarvyn, så kod som är beroende av att användarna trycker på spelarvyn fungerar inte.
* Anrop om att pausa och spela upp spelarinstansen pausar och återupptar VPAID-annonsen.
* VPAID-annonser har ingen fördefinierad varaktighet eftersom annonsen kan vara interaktiv.

   Annonsens längd och varaktighet för den totala annonsbrytningen som anges i annonsserversvaret kanske inte är korrekt.