---
description: En MediaResource representerar det innehåll som ska läsas in av MediaPlayer-instansen.
seo-description: En MediaResource representerar det innehåll som ska läsas in av MediaPlayer-instansen.
seo-title: Klasserna MediaPlayer och MediaResource
title: Klasserna MediaPlayer och MediaResource
uuid: 36ef75f3-08f7-4fc5-88a7-9bab9198b917
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Klasserna MediaPlayer och MediaResource{#mediaplayer-and-mediaresource-classes}

En MediaResource representerar det innehåll som ska läsas in av MediaPlayer-instansen.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK-biblioteket erbjuder ett enkelt sätt att läsa in och förbereda innehåll för uppspelning genom att använda metoden `replaceCurrentResource` i gränssnittet `MediaPlayer`. Den här metoden tar emot en instans av klassen `MediaResource` som det enda indataargumentet. Klassen `MediaResource` består av följande information:

* En URL, som representerar platsen för innehållet som ska läsas in.
* En typ, som är den typ av innehåll som ska läsas in.

   Detta är en sträng som definierar de typer av innehåll som kan läsas in av `MediaPlayer`. Möjliga värden är HLS och HDS. Varje värde är associerat med strängen som representerar de filtillägg som vanligtvis används, &quot;m3u8&quot; för HLS och &quot;f4m&quot; för HDS.
* Vissa metadata, som är en instans av klassen `Metadata`.

   Den här ordlisteliknande strukturen kan innehålla ytterligare information om innehållet som ska läsas in, till exempel information om alternativ-/annonsinnehållet som ska placeras i huvudinnehållet.

Metadata är det medium genom vilket information som är relaterad till alternativt innehåll skickas till TVSDK. Gränssnittet `Metadata` definierar API:t för ett generiskt nyckelvärdeslager, där både nyckeln och värdet är rena strängar.
