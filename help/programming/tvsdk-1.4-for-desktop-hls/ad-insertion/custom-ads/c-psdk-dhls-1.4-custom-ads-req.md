---
description: Video Player Ad-Serving Interface Definition (VPAID) är ett gemensamt gränssnitt för att spela upp videoannonser. VPAID ger en multimedieupplevelse för användarna och ger utgivaren möjlighet att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll.
seo-description: Video Player Ad-Serving Interface Definition (VPAID) är ett gemensamt gränssnitt för att spela upp videoannonser. VPAID ger en multimedieupplevelse för användarna och ger utgivaren möjlighet att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll.
seo-title: Anpassade annonskrav
title: Anpassade annonskrav
uuid: 6d4ba87b-ffe5-467d-8ab5-9795928c2f69
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Anpassade annonskrav {#custom-ad-requirements}

TVSDK-spelaren kan spela upp VPAID-annonser (Digital Video Player Ad-Interface Definition) och visa annonsens inläsningsstatus. Om det finns fel i annonsen, eller om det tar för lång tid att läsa in annonser, ignorerar TVSDK dessa annonser.

Video Player Ad-Serving Interface Definition (VPAID) är ett gemensamt gränssnitt för att spela upp videoannonser. VPAID ger en multimedieupplevelse för användarna och ger utgivaren möjlighet att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll.

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

TVSDK har stöd för följande funktioner:

* Version 1.0 och 2.0 av VPAID-specifikationen
* Linjära VPAID-annonser om VOD-innehåll (video-on-demand)
* Flash VPAID-annonser

   VPAID-annonser måste vara Flash-baserade, och annonssvaret måste identifiera medietypen för VPAID-annonsen som `application/x-shockwave-flash`.

Följande funktioner stöds inte:

* Annonser som övertäckningar och dynamiska följesedlar
* Förhandsladda VPAID-annonser
* VPAID-annonser i direktinnehåll
* JavaScript VPAID-annonser

## Läser in status {#section_5F55C0101CD44A65BCFE1D124CBDF239}

TVSDK skickar följande händelser:

* `AdLoading`
* `AdLoaded`
* `AdStarted`
* `AdPlaying`
* `AdStopped`

Efter `AdStopped` händelsen återupptar TVSDK videoinnehållet.

>[!TIP]
>
>Om du anger värdet noll försöker TVSDK läsa in annonsen tills den läses in eller ett fel har inträffat.

## Ignorerar annonser {#section_3EA452F420884335AE90DF23C17E416A}

Om annonsen tar för lång tid att läsa in eller om det finns fel i annonsen, kan TVSDK ignorera annonsen och nästa annons i annonsuppsättningen spelas upp automatiskt.

Om `AuditudeSettings.customAdLoadTimeout` inställningen anger ett antal sekunder som är större än noll försöker TVSDK läsa in annonsen till den angivna längden. Om annonsen inte kan läsas in hoppas annonsen över. Om du till exempel konfigurerar `AuditudeSettings.customAdLoadTimeout:5`försöker TVSDK att läsa in annonsen i högst 5 sekunder. Om annonsen fortfarande inte läses in ignoreras den.
