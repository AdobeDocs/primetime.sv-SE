---
description: Du kan få en beskrivning av tidslinjen som är associerad med det markerade objekt som spelas upp av TVSDK. Detta är mest användbart när programmet visar en anpassad navigeringsfältskontroll där innehållsavsnitt som motsvarar annonsinnehåll identifieras.
title: Inspect tidslinjen för uppspelning
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Inspect tidslinjen för uppspelning{#inspect-the-playback-timeline}

Du kan få en beskrivning av tidslinjen som är associerad med det markerade objekt som spelas upp av TVSDK. Detta är mest användbart när programmet visar en anpassad navigeringsfältskontroll där innehållsavsnitt som motsvarar annonsinnehåll identifieras.

Här är ett exempel på implementering som visas i följande skärmbild.
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. Kom åt `Timeline`-objektet i `MediaPlayer` med metoden `get`.

   Klassen `Timeline` kapslar in informationen som är relaterad till innehållet i tidslinjen som är associerad med mediaobjektet som för närvarande är inläst av `MediaPlayer`-instansen. Klassen `Timeline` ger åtkomst till en skrivskyddad vy av den underliggande tidslinjen. Klassen `Timeline` innehåller en get-metod för att hämta alla monterade `TimelineMarker`-objekt.

1. Iterera genom listan med `TimelineMarkers` och använd den returnerade informationen för att implementera tidslinjen.

       Ett TimelineMarker-objekt innehåller två informationsdelar:
   
   * Markörens position på tidslinjen (i millisekunder)
   * Markörens varaktighet på tidslinjen (i millisekunder)

<!--<a id="example_BA936629E82B4082A2E2C548E3FC3357"></a>-->

```
// access the timeline object 
var timeline:Timeline = mediaPlayer.timeline; 
 
// iterate through the list of TimelineMarkers 
var markers:Vector.<TimelineMarker> = timeline.timelineMarkers; 
markers.forEach(function(item:TimelineMarker,  
                         index:int,  
                         vector:Vector.<TimelineMarker>):void { 
    
    // the start position of the marker 
    var startPos:Number = item.time; 
 
    // the duration of the marker 
    var duration:Number = item.duration; 
 
    // draw the marker on the scrub-bar 
}
```

