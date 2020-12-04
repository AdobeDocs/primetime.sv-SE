---
description: Om du vill använda TVSDK så effektivt som möjligt bör du ta hänsyn till vissa detaljer i hur TVSDK fungerar och följa vissa bästa metoder.
seo-description: Om du vill använda TVSDK så effektivt som möjligt bör du ta hänsyn till vissa detaljer i hur TVSDK fungerar och följa vissa bästa metoder.
seo-title: Överväganden och bästa praxis
title: Överväganden och bästa praxis
uuid: 62a5d641-6f37-4e4d-bbc2-414bf3681d9c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Överväganden och bästa praxis{#considerations-and-best-practices}

Om du vill använda TVSDK så effektivt som möjligt bör du ta hänsyn till vissa detaljer i hur TVSDK fungerar och följa vissa bästa metoder.

## Överväganden {#section_tvsdk_considerations}

Kom ihåg följande information när du använder TVSDK:

* Adobe Primetime fungerar inte med emulatorer eller simulatorer.

   Du måste använda riktiga enheter för testning.
* Uppspelning stöds endast för HTTP-direktuppspelning (HLS).
* Huvudinnehållet i videon kan multiplexas, där video- och ljudströmmar finns i samma återgivning, eller inte multiplexas, där video- och ljudströmmar finns i separata återgivningar.
* TVSDK-API:t implementeras i ActionScript.
* Videouppspelning kräver Adobe Video Engine (AVE). Detta påverkar hur och när medieresurser kan nås:

   * Undertexter stöds i den utsträckning som AVE tillhandahåller.
   * Beroende på kodningsprecisionen kan den faktiska längden för kodade medier skilja sig från varaktigheten som registreras i strömmens resursmanifest.

      Det finns inget tillförlitligt sätt att synkronisera om mellan den idealiska virtuella tidslinjen och den faktiska tidslinjen för uppspelning. Förloppsspårning för direktuppspelning för annonshantering och videoanalys måste använda den faktiska uppspelningstiden, så rapporterings- och användargränssnittets beteende kanske inte spårar medie- och reklaminnehållet exakt.
   * Inkommande användaragentnamn för alla HTTP-begäranden från TVSDK på den här plattformen tilldelas följande strängmönster:

      ```
      "Adobe Flash Player"
      ```

## God praxis {#section_tvsdk_best_practices}

Här är de rekommenderade metoderna för TVSDK:

* Använd HLS version 3.0 eller senare för programinnehåll.
* För TVSDK 1.4 för DHLS är lat och inläsning aktiverat som standard.

   För innehåll utan pre-roll eller middle-roll kan du använda `AdvertisingMetadata.delayAdLoading` för att snabba upp inläsningen av innehåll ytterligare.

