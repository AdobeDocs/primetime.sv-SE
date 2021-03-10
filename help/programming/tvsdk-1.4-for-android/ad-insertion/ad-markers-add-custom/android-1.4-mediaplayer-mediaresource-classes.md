---
description: En MediaResource representerar det innehåll som ska läsas in av MediaPlayer-instansen.
title: Klasserna MediaPlayer och MediaResource
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Klasserna MediaPlayer och MediaResource{#mediaplayer-and-mediaresource-classes}

En MediaResource representerar det innehåll som ska läsas in av MediaPlayer-instansen.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK-biblioteket är ett enkelt sätt att läsa in och förbereda innehåll för uppspelning med metoden `replaceCurrentItem` i MediaPlayer-gränssnittet. Den här metoden tar emot en instans av MediaResource-klassen som det enda indataregumentet. Klassen MediaResource består av följande information:

* En URL, som representerar platsen för innehållet som ska läsas in.
* En typ, som är den typ av innehåll som ska läsas in.

   Detta är en enkel uppräkning i klassen `MediaResource` som definierar de typer av innehåll som kan läsas in av MediaPlayer. Möjliga värden är HLS och HDS. Varje värde är associerat med strängen som representerar de filtillägg som ofta används, `m3u8` för HLS och `f4m` för HDS.
* Vissa metadata, som är en instans av klassen `Metadata`.

   Den här ordlisteliknande strukturen kan innehålla ytterligare information om innehållet som ska läsas in, till exempel information om alternativ-/annonsinnehållet som ska placeras i huvudinnehållet.

Metadata är det medium genom vilket information som är relaterad till alternativt innehåll skickas till TVSDK. Gränssnittet `Metadata` definierar API:t för ett generiskt nyckelvärdeslager, där både nyckeln och värdet är rena strängar.
