---
description: Det finns några sätt att avgöra annonsinfogning och annonsplacering.
seo-description: Det finns några sätt att avgöra annonsinfogning och annonsplacering.
seo-title: Infogning och placering av annonser
title: Infogning och placering av annonser
uuid: 1d4d6364-1c49-402b-9b72-8c185b1c94e1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Infogning och placering av annonser{#ad-insertion-and-placement}

Det finns några sätt att avgöra annonsinfogning och annonsplacering.

## Annonsinfogning {#section_1F7581B987704E318E064082190E8243}

Här är en översikt över processen som används för att bestämma annonsinfogning:

1. **Affärsmöjlighet**: TVSDK använder ströminformation för att identifiera möjliga och önskade platser för annonser.
1. **Annonsupplösning**: TVSDK kommunicerar med en annonsserver för att hämta annonser som ska delas in i innehållet.
1. **Annonsplacering**: TVSDK läser in de angivna annonserna och placerar dem i annonsbrytningar på innehållets tidslinje på de angivna platserna och beräknar om den virtuella tidslinjen, om det behövs.

## Annonsplacering {#section_B9D63F7409A2447F9FF209289BE5D3D5}

TVSDK kan hämta platser för annonsplacering från följande källor:

* **Manifestets metadata/cues**

   TVSDK identifierar ledtrådarna, extraherar nödvändig information från dessa ledtrådar och kommunicerar med en annonsserver för att få motsvarande annonser. Den här källan är vanlig för live/linjära strömmar.

   TVSDK ersätter vanligtvis huvudinnehållet med annonserna på den plats som anges av metadata/ledtrådarna. i annat fall skulle kunden mer och mer lägga sig bakom den verkliga direktpunkten.

* **Marknadsföringsserverns karta**

   Vanligtvis registreras metadata om dessa strömmar på annonsservern innan de spelas upp. TVSDK hämtar annonstidslinjen och motsvarande annonser från servern. Den här källan är vanlig för VOD-strömmar.

   TVSDK infogar vanligtvis lösta annonser i huvudinnehållet enligt serverkartan.

>[!NOTE]
>
>Som standard använder TVSDK manifesttecken för live/linjära strömmar och annonsserverkartor för VOD-strömmar. Om du vill ha stöd för reprisering av live-event måste programmet dock vidta extra åtgärder.

