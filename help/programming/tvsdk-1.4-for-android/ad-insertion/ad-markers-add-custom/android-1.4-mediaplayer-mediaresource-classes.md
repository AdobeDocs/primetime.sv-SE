---
description: En MediaResource representerar det innehåll som ska läsas in av MediaPlayer-instansen.
title: Klasserna MediaPlayer och MediaResource
exl-id: d3ac1a8d-3549-417a-83e9-c561a3d12127
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Klasserna MediaPlayer och MediaResource{#mediaplayer-and-mediaresource-classes}

En MediaResource representerar det innehåll som ska läsas in av MediaPlayer-instansen.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK-biblioteket är ett enkelt sätt att läsa in och förbereda innehåll för uppspelning med `replaceCurrentItem` i MediaPlayer-gränssnittet. Den här metoden tar emot en instans av MediaResource-klassen som det enda indataregumentet. Klassen MediaResource består av följande information:

* En URL, som representerar platsen för innehållet som ska läsas in.
* En typ, som är den typ av innehåll som ska läsas in.

   Det här är en enkel uppräkning i `MediaResource` -klass som definierar de typer av innehåll som kan läsas in av MediaPlayer. Möjliga värden är HLS och HDS. Varje värde är associerat med strängen som representerar de filtillägg som används ofta. `m3u8` för HLS och `f4m` för HDS.
* Vissa metadata, som är en instans av `Metadata` klassen.

   Den här ordlisteliknande strukturen kan innehålla ytterligare information om innehållet som ska läsas in, till exempel information om alternativ-/annonsinnehållet som ska placeras i huvudinnehållet.

Metadata är det medium genom vilket information som är relaterad till alternativt innehåll skickas till TVSDK. The `Metadata` -gränssnittet definierar API:t för ett generiskt nyckelvärdeslager, där både nyckeln och värdet är rena strängar.
