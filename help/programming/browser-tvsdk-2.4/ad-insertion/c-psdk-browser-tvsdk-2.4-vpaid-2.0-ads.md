---
description: VPAID 2.0 (Video Player ad-sting interface definition) ger ett gemensamt gränssnitt för att spela upp videoannonser. Det ger en multimedieupplevelse för användarna och gör det möjligt för utgivare att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll.
title: Stöd för VPAID 2.0
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Stöd för VPAID 2.0 {#vpaid-ad-support}

VPAID 2.0 (Video Player ad-sting interface definition) ger ett gemensamt gränssnitt för att spela upp videoannonser. Det ger en multimedieupplevelse för användarna och gör det möjligt för utgivare att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll.

Följande funktioner stöds:

* Version 2.0 av VPAID-specifikationen

  Mer information finns i [IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/).
* Linjära VPAID-annonser med VOD-innehåll (video on demand)
* I Live-innehåll har Browser TVSDK stöd för JavaScript VPAID-annonser före användning.
* I Flashens felsökningsläge stöder webbläsarens TVSDK endast Flash-baserade VPAID-annonser.
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

* The `getCustomAdView` metod för `MediaPlayer` returnerar `CustomAdView` -objekt, som representerar den webbvy som återger VPAID-annonsen.

  Mer information om `getCustomAdView` metod, se [MediaPlayer API-dokumentation](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` anger timeout för VPAID-inläsningsprocessen.

  Standardvärdet för timeout är 10 sekunder.

* API:t `auditudeSettings.ignoreVPAIDAds`kan du ignorera VPAID-annonser som tagits emot från Auditude-servern. API:t fungerar inte för Flash Fallback.

Medan VPAID-annonsen spelas:

* VPAID-annonsen visas i en visningsbehållare ovanför spelarvyn, så kod som är beroende av att användarna trycker på spelarvyn fungerar inte.
* Anrop om att pausa och spela upp spelarinstansen pausar och återupptar VPAID-annonsen.
* VPAID-annonser har ingen fördefinierad varaktighet eftersom annonsen kan vara interaktiv.

  Annonsens längd och varaktighet för den totala annonsbrytningen som anges i annonsserversvaret kanske inte är korrekt.
