---
description: Om du vill använda TVSDK så effektivt som möjligt bör du ta hänsyn till vissa detaljer i hur TVSDK fungerar och följa vissa bästa metoder.
seo-description: Om du vill använda TVSDK så effektivt som möjligt bör du ta hänsyn till vissa detaljer i hur TVSDK fungerar och följa vissa bästa metoder.
seo-title: Överväganden och bästa praxis
title: Överväganden och bästa praxis
uuid: e698ae09-280b-4406-a9b8-4f468b7a6b9c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Överväganden och bästa praxis{#considerations-and-best-practices}

Om du vill använda TVSDK så effektivt som möjligt bör du ta hänsyn till vissa detaljer i hur TVSDK fungerar och följa vissa bästa metoder.

## Överväganden {#section_tvsdk_considerations}

Kom ihåg följande information när du använder TVSDK:

* Adobe Primetime fungerar för närvarande inte på Android-emulatorer.

   Du måste använda riktiga enheter för testning.
* Uppspelning stöds endast för HTTP-direktuppspelning (HLS).
* Huvudinnehållet i videon kan multiplexas, där video- och ljudströmmar finns i samma återgivning, eller inte multiplexas, där video- och ljudströmmar finns i separata återgivningar.
* TVSDK-API:t implementeras i Java.
* För närvarande måste du köra de flesta TVSDK API-åtgärder på gränssnittstråden, som är Android-huvudtråden.

   Åtgärder som körs korrekt på huvudtråden kan orsaka ett fel och avslutas när de körs på en bakgrundstråd.
* Videouppspelning kräver Adobe Video Engine (AVE). Detta påverkar hur och när medieresurser kan nås:

   * Undertexter stöds i den utsträckning som AVE tillhandahåller.
   * Beroende på kodningsprecisionen kan den faktiska längden för kodade medier skilja sig från varaktigheten som registreras i strömmens resursmanifest.

      Det finns inget tillförlitligt sätt att återsynkronisera mellan den idealiska virtuella tidslinjen och den faktiska tidslinjen för uppspelning. Förloppsspårning för direktuppspelning för annonshantering och videoanalys måste använda den faktiska uppspelningstiden, så rapporterings- och användargränssnittets beteende kanske inte spårar medie- och reklaminnehållet exakt.
   * Inkommande användaragentnamn för alla mediebegäranden från TVSDK på den här plattformen tilldelas följande strängmönster:

      ```
      "Adobe Primetime/ + 
      <varname>
      originalUserAgent
      </varname>" 
      ```

      Alla annonsrelaterade anrop använder Androids standardanvändaragent eller den anpassade användaragenten om du ställer in den när du ställer in metadata för annonsinfogning.

## God praxis {#section_tvsdk_best_practices}

Här följer rekommenderad praxis för TVSDK:

* Använd HLS version 3.0 eller senare för programinnehåll.
* Kör de flesta TVSDK-åtgärder i huvudtråden (UI), inte på bakgrundstrådar.
