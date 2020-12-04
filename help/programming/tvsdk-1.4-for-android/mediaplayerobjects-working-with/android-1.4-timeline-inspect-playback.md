---
description: Du kan få en beskrivning av tidslinjen som är associerad med det markerade objekt som spelas upp av TVSDK. Detta är mest användbart när programmet visar en anpassad navigeringsfältskontroll där innehållsavsnitt som motsvarar annonsinnehåll identifieras.
seo-description: Du kan få en beskrivning av tidslinjen som är associerad med det markerade objekt som spelas upp av TVSDK. Detta är mest användbart när programmet visar en anpassad navigeringsfältskontroll där innehållsavsnitt som motsvarar annonsinnehåll identifieras.
seo-title: Inspect tidslinjen för uppspelning
title: Inspect tidslinjen för uppspelning
uuid: b5ede131-1037-449b-bc3f-a066fdc92fc5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# Inspect tidslinjen för uppspelning{#inspect-the-playback-timeline}

Du kan få en beskrivning av tidslinjen som är associerad med det markerade objekt som spelas upp av TVSDK. Detta är mest användbart när programmet visar en anpassad navigeringsfältskontroll där innehållsavsnitt som motsvarar annonsinnehåll identifieras.

Här är ett exempel på implementering som visas i följande skärmbild.  ![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. Kom åt `Timeline`-objektet i `MediaPlayer` med metoden `getTimeline`.

   Klassen `Timeline` kapslar in informationen som är relaterad till innehållet i tidslinjen som är associerad med mediaobjektet som för närvarande är inläst av `MediaPlayer`-instansen. Klassen `Timeline` ger åtkomst till en skrivskyddad vy av den underliggande tidslinjen. Klassen `Timeline` innehåller en get-metod som ger en iterator genom en lista med `TimelineMarker`-objekt.

1. Iterera genom listan med `TimelineMarkers` och använd den returnerade informationen för att implementera tidslinjen.

       Ett TimelineMarker-objekt innehåller två informationsdelar:
   
   * Markörens position på tidslinjen (i millisekunder)
   * Markörens varaktighet på tidslinjen (i millisekunder)

1. Implementera avlyssnargränssnittet `MediaPlayer.PlaybackEventListener.onTimelineUpdated` och registrera det med objektet `Timeline`.

   `Timeline`-objektet kan informera programmet om ändringar som kan inträffa på tidslinjen för uppspelningen genom att anropa `OnTimelineUpdated`-avlyssnaren.

```java
// access the timeline object 
Timeline timeline = mediaPlayer.getTimeline(); 
// iterate through the list of TimelineMarkers 
Iterator<TimelineMarker> iterator = timeline.timelineMarkers(); 
while (iterator.hasNext()) { 
   TimelineMarker marker = iterator.next(); 
   // the start position of the marker 
   long startPos = marker.getTime(); 
   // the duration of the marker 
   long duration = marker.getDuration(); 
}
```

