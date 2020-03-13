---
description: VPAID 2.0 (Video Player ad-sting interface definition) ger ett gemensamt gränssnitt för att spela upp videoannonser. Det ger en multimedieupplevelse för användarna och gör det möjligt för utgivare att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll.
seo-description: VPAID 2.0 (Video Player ad-sting interface definition) ger ett gemensamt gränssnitt för att spela upp videoannonser. Det ger en multimedieupplevelse för användarna och gör det möjligt för utgivare att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll.
seo-title: Stöd för VPAID 2.0
title: Stöd för VPAID 2.0
uuid: 6485e387-2a13-476f-a0fd-91c6e19fd385
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Stöd för VPAID 2.0 {#vpaid-ad-support}

VPAID 2.0 (Video Player ad-sting interface definition) ger ett gemensamt gränssnitt för att spela upp videoannonser. Det ger en multimedieupplevelse för användarna och gör det möjligt för utgivare att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll.

Följande funktioner stöds:

* Version 2.0 av VPAID-specifikationen

   Mer information finns i [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Linjära VPAID-annonser med VOD-innehåll (video on demand)
* JavaScript VPAID-annonser

   VPAID-annonser måste vara JavaScript-baserade, och annonssvaret måste identifiera medietypen för VPAID-annonsen som `application/javascript`.

Följande funktioner stöds inte:

* Version 1.0 av VPAID-specifikationen
* Överhoppade annonser
* Annonser som inte finns online, som överläggsannonser, dynamiska följeslagarannonser, minimeringsbara annonser, komprimerbara annonser och expanderbara annonser
* Förhandsladda VPAID-annonser
* VPAID-annonser i direktinnehåll
* Flash VPAID-annonser

## API

Följande API-element stöder VPAID 2.0-annonser:

* Metoden `getCustomAdView` för att `MediaPlayer` returnera ett `CustomAdView` objekt, som representerar den webbvy som återger VPAID-annonsen (se [API-referenser](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/index.html)).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` anger timeout för VPAID-inläsningsprocessen. Standardvärdet för timeout är 10 sekunder.

Under uppspelningen av VPAID-annonsen:

* VPAID-annonsen visas i en visningsbehållare ovanför spelarvyn, så kod som är beroende av att användarna trycker på spelarvyn fungerar inte.
* Anrop till `pause` och `play` på spelarinstansen pausar och återupptar VPAID-annonsen.

* VPAID-annonser har ingen fördefinierad varaktighet eftersom annonsen kan vara interaktiv.

   Annonsens längd och varaktighet för den totala annonsbrytningen som anges i annonsserversvaret kanske inte är korrekt.