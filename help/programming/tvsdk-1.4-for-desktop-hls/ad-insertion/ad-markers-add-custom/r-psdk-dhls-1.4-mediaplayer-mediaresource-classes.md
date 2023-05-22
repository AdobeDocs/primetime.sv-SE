---
description: En MediaResource representerar det innehåll som ska läsas in av MediaPlayer-instansen.
title: Klasserna MediaPlayer och MediaResource
exl-id: c431c9f9-98a3-402c-b799-450f30f668dd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Klasserna MediaPlayer och MediaResource{#mediaplayer-and-mediaresource-classes}

En MediaResource representerar det innehåll som ska läsas in av MediaPlayer-instansen.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK-biblioteket är ett enkelt sätt att läsa in och förbereda innehåll för uppspelning med `replaceCurrentResource` metoden i `MediaPlayer` gränssnitt. Den här metoden tar emot en instans av `MediaResource` -klassen som det enda indataargumentet. The `MediaResource` klassen består av följande information:

* En URL, som representerar platsen för innehållet som ska läsas in.
* En typ, som är den typ av innehåll som ska läsas in.

   Detta är en sträng som definierar de typer av innehåll som kan läsas in av `MediaPlayer`. Möjliga värden är HLS och HDS. Varje värde är associerat med strängen som representerar de filtillägg som vanligtvis används, &quot;m3u8&quot; för HLS och &quot;f4m&quot; för HDS.
* Vissa metadata, som är en instans av `Metadata` klassen.

   Den här ordlisteliknande strukturen kan innehålla ytterligare information om innehållet som ska läsas in, till exempel information om alternativ-/annonsinnehållet som ska placeras i huvudinnehållet.

Metadata är det medium genom vilket information som är relaterad till alternativt innehåll skickas till TVSDK. The `Metadata` -gränssnittet definierar API:t för ett generiskt nyckelvärdeslager, där både nyckeln och värdet är rena strängar.
