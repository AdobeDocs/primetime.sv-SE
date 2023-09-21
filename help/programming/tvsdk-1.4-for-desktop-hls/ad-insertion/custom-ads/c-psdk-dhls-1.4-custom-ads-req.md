---
description: Video Player Ad-Serving Interface Definition (VPAID) är ett gemensamt gränssnitt för att spela upp videoannonser. VPAID ger en multimedieupplevelse för användarna och ger utgivaren möjlighet att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll.
title: Anpassade annonskrav
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Anpassade annonskrav {#custom-ad-requirements}

TVSDK-spelaren kan spela upp VPAID-annonser (Digital Video Player Ad-Interface Definition) och visa annonsens inläsningsstatus. Om det finns fel i annonsen, eller om det tar för lång tid att läsa in annonser, ignorerar TVSDK dessa annonser.

Video Player Ad-Serving Interface Definition (VPAID) är ett gemensamt gränssnitt för att spela upp videoannonser. VPAID ger en multimedieupplevelse för användarna och ger utgivaren möjlighet att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll.

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

TVSDK stöder följande funktioner:

* Version 1.0 och 2.0 av VPAID-specifikationen
* Linjära VPAID-annonser om VOD-innehåll (video-on-demand)
* Flash VPAID-annonser

  VPAID-annonser måste vara Flash-baserade, och annonseringssvaret måste identifiera medietypen för VPAID-annonsen som `application/x-shockwave-flash`.

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

Efter `AdStopped` -händelsen återupptar TVSDK videoinnehållet.

>[!TIP]
>
>Om du anger värdet noll försöker TVSDK läsa in annonsen tills den läses in eller ett fel har inträffat.

## Ignorerar annonser {#section_3EA452F420884335AE90DF23C17E416A}

Om annonsen tar för lång tid att läsa in eller om det finns fel i annonsen, kan TVSDK ignorera annonsen och nästa annons i annonsuppsättningen spelas upp automatiskt.

Om `AuditudeSettings.customAdLoadTimeout` -inställningen anger ett antal sekunder som är större än noll, kommer TVSDK att försöka läsa in annonsen till den angivna varaktigheten. Om annonsen inte kan läsas in hoppas annonsen över. Om du till exempel konfigurerar `AuditudeSettings.customAdLoadTimeout:5`, försöker TVSDK att läsa in annonsen i högst fem sekunder. Om annonsen fortfarande inte läses in ignoreras den.
