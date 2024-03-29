---
description: CRS erbjuder JIT (just-in-time) och asynkron ompaketering och HLS-to-HLS-konvertering. Resultatet av ompaketeringen är en HLS-formaterad version av den ursprungliga annonsdesignen. CRS placerar den HLS-formaterade versionen på CDN-servern (Content Delivery Network) för användning vid behov.
title: Huvudsaklig användning av CRS
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Huvudsaklig användning av CRS {#main-uses-of-crs}

CRS erbjuder JIT (just-in-time) och asynkron ompaketering och HLS-to-HLS-konvertering. Resultatet av ompaketeringen är en HLS-formaterad version av den ursprungliga annonsdesignen. CRS placerar den HLS-formaterade versionen på CDN-servern (Content Delivery Network) för användning vid behov.

I JIT-ompaketering av Adobe Primetime-annonsinfogningen börjar ompaketeringsprocessen när en person som inte är HLS eller kreativ påträffas. Detta innebär vanligtvis förlorade möjligheter att köra annonsen under ompaketeringsprocessen.

Vid asynkron ompackning omkodas annonspersonalen och lagras innan den behövs, vilket kan eliminera de förlorade möjligheterna.

Vid HLS-till-HLS-konvertering formaterar CRS om en HLS och kreativa enheter till lämpliga segment för att säkerställa en konsekvent uppspelning.

## Just-in-Time Repackaging {#section_1BA344F2300B49F291865A7461EDFEAE}

Sekvensen för JIT-ompaketering är följande:

1. Manifestservern hämtar en annons.
1. Om annonsformatet är HLS infogar manifestservern annonsen i innehållsströmmen.
1. Om formatet inte är HLS (till exempel MP4, FLV eller WebM) söker manifestservern efter en omkodad version på CDN-servern. Om den hittar en infogar den omkodade annonsen i innehållsströmmen.
1. Om formatet inte är HLS och CDN-servern inte har någon omkodad version skickar manifestservern annonsen till CRS, som omkodar annonsens kreativitet och lagrar resultatet på CDN-servern för senare bruk.
1. Manifestservern returnerar innehållet utan annonsen.

## Asynkron ompackning {#section_ACDFB43FDA4B445CB9F2A107FEB4F2F7}

Du kan använda API:t som beskrivs i [API för ompaketering](../~old-creative-repackaging-service/api-repackage.md) förkoda en icke-HLS-kreativ för att minimera förlust av visningar och maximera intäktsgenereringen.

## HLS-till-HLS-konvertering {#section_877A0E7E8FAF4C2DB086A31C24D53435}

För att undvika buffring och fördröjning hämtar en klient en video i små segment. Om segmentstorlekarna är inkonsekventa kan uppspelningen bli ryckig. HLS-till-HLS-konvertering säkerställer att datasegmenten har samma varaktighet (till exempel 6 sekunder).

>[!NOTE]
>
>CRS skapar HLS version 3, oavsett vilken HLS-version den tar emot.