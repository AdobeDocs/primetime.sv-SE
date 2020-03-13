---
description: Om du vill använda TVSDK så effektivt som möjligt bör du ta hänsyn till vissa detaljer i hur TVSDK fungerar och följa vissa bästa metoder.
seo-description: Om du vill använda TVSDK så effektivt som möjligt bör du ta hänsyn till vissa detaljer i hur TVSDK fungerar och följa vissa bästa metoder.
seo-title: Överväganden och bästa praxis
title: Överväganden och bästa praxis
uuid: b37a5710-e811-4c3e-be8c-7c34ee5944e5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Överväganden och bästa praxis{#considerations-and-best-practices}

Om du vill använda TVSDK så effektivt som möjligt bör du ta hänsyn till vissa detaljer i hur TVSDK fungerar och följa vissa bästa metoder.

## Överväganden {#section_tvsdk_considerations}

Kom ihåg följande information när du använder TVSDK:

* Adobe Primetime fungerar inte i iOS-simulatorer.

   Du måste använda riktiga enheter för testning.
* Uppspelning stöds endast för HTTP-direktuppspelning (HLS).
* Huvudinnehållet kan multiplexas, där video- och ljudströmmar finns i samma återgivning, eller icke-multiplexat, där video- och ljudströmmar finns i separata återgivningar.
* TVSDK-API:t implementeras i mål-C.
* Videouppspelning kräver det inbyggda Apple AV Foundation-ramverket. Detta påverkar hur och när medieresurser, inklusive undertexter och tidslinjer, kan nås:

   * Det går inte att ändra tidslinjejusteringar efter den första konfigurationen.

      En annons kan till exempel inte tas bort från tidslinjen efter att den har spelats upp. Om användaren söker tillbaka i presentationen spelas samma annons upp igen även om policyn skulle ha varit att ta bort annonsen.
   * Beroende på kodningsprecisionen kan den faktiska längden för kodade medier skilja sig från varaktigheten som registreras i strömmens resursmanifest.

      Det finns inget tillförlitligt sätt att synkronisera om mellan den idealiska virtuella tidslinjen och den faktiska tidslinjen för uppspelning. Förloppsspårning för direktuppspelning för annonshantering och videoanalys måste använda den faktiska uppspelningstiden, så rapporterings- och användargränssnittets beteende kanske inte spårar medie- och reklaminnehållet exakt.
   * Den inkommande användaragenten för alla HTTP-begäranden från TVSDK på den här plattformen bestäms av enheten och iOS-versionen som körs på enheten.

      Standardvärdet för användaragentsträngen är det som tilldelas av operativsystemet.

## God praxis {#section_tvsdk_best_practices}

Här följer rekommenderad praxis för TVSDK:

* Använd HLS version 3.0 eller senare för programinnehåll.
* Använd Apples mediastreamvalidator för att validera VOD-strömmar.
* Klassen innehåller metoder för att framtvinga SSL på begäranden som görs till Primetimes annonsbesluts-, DRM- och Video Analytics-servrar. `PTSDKConfig`

   Mer information finns i avsnitten om `forceHTTPS` och `isForcingHTTPS` metoder i den här klassen.

   >[!IMPORTANT]
   >
   >Begäranden till tredjepartsdomäner som annonsspårning av pixlar, innehålls- och annonsadresser och liknande begäranden ändras inte. Innehållsleverantörerna och annonsservrarna ansvarar för att tillhandahålla URL:er som stöds via HTTPS.

