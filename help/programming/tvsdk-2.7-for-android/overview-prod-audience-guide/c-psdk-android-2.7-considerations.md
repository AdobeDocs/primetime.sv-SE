---
description: Om du vill använda TVSDK så effektivt som möjligt bör du ta hänsyn till vissa detaljer i hur TVSDK fungerar och följa vissa bästa metoder.
title: Överväganden och bästa praxis
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# Överväganden och bästa praxis{#considerations-and-best-practices}

Om du vill använda TVSDK så effektivt som möjligt bör du ta hänsyn till vissa detaljer i hur TVSDK fungerar och följa vissa bästa metoder.

## Överväganden {#section_tvsdk_considerations}

Kom ihåg följande information när du använder TVSDK:

* TVSDK-API:t implementeras i Java.
* Adobe Primetime fungerar för närvarande inte på Android-emulatorer.

   Du måste använda riktiga enheter för testning.
* Uppspelning stöds endast för HTTP-direktuppspelning (HLS).
* Huvudvideoinnehåll kan multiplexas (video- och ljudströmmar i samma återgivning) eller icke-multiplexat (video- och ljudströmmar i separata återgivningar).
* För närvarande måste du köra de flesta TVSDK API-åtgärder på gränssnittstråden, som är Android-huvudtråden.

   Åtgärder som körs korrekt på huvudtråden kan orsaka ett fel och avslutas när de körs på en bakgrundstråd.
* Videouppspelning kräver Adobe Video Engine (AVE). Detta påverkar hur och när medieresurser kan nås:

   * Undertexter stöds i den utsträckning som AVE tillhandahåller.
   * Beroende på kodningsprecisionen kan den faktiska längden för kodade medier skilja sig från varaktigheten som registreras i strömmens resursmanifest.

      Det finns inget tillförlitligt sätt att synkronisera om mellan den idealiska virtuella tidslinjen och den faktiska tidslinjen för uppspelning. Förloppsspårning för direktuppspelning för annonshantering och videoanalys måste använda den faktiska uppspelningstiden, så rapporterings- och användargränssnittets beteende kanske inte spårar medie- och reklaminnehållet exakt.
   * Inkommande användaragentnamn för alla mediebegäranden från TVSDK på den här plattformen tilldelas följande strängmönster:

   ```
   "Adobe Primetime/" + 
   <varname>
   originalUserAgent
   </varname> 
   ```

   Alla annonsrelaterade anrop använder Androids standardanvändaragent eller den anpassade användaragenten om du ställer in den när du ställer in metadata för annonsinfogning.

## God praxis {#section_tvsdk_best_practices}

Här följer rekommenderad praxis för TVSDK:

* Använd HLS version 3.0 eller senare för programinnehåll.
* Kör de flesta TVSDK-åtgärder på huvudtråden (UI), inte på bakgrundstrådar.
* För TVSDK 2.5 för Android är&quot;lat&quot; och matchande&quot; aktiverat som standard.

   För innehåll utan pre-roll eller middle-roll kan du använda `AdvertisingMetadata.setPreroll(false)` för att snabba upp inläsningen av innehåll.
