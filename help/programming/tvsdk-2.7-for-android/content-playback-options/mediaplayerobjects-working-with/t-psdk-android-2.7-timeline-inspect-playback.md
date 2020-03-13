---
description: Du kan få en beskrivning av tidslinjen som är associerad med det markerade objekt som spelas upp av TVSDK. Detta är mest användbart när programmet visar en anpassad navigeringsfältskontroll där innehållsavsnitt som motsvarar annonsinnehåll identifieras.
seo-description: Du kan få en beskrivning av tidslinjen som är associerad med det markerade objekt som spelas upp av TVSDK. Detta är mest användbart när programmet visar en anpassad navigeringsfältskontroll där innehållsavsnitt som motsvarar annonsinnehåll identifieras.
seo-title: Inspektera tidslinjen för uppspelning
title: Inspektera tidslinjen för uppspelning
uuid: d0fe7926-9b9a-4203-a1c7-e57ba25b882e
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Inspektera tidslinjen för uppspelning {#inspect-the-playback-timeline}

Du kan få en beskrivning av tidslinjen som är associerad med det markerade objekt som spelas upp av TVSDK. Detta är mest användbart när programmet visar en anpassad navigeringsfältskontroll där innehållsavsnitt som motsvarar annonsinnehåll identifieras.

Här är ett exempel på implementering som visas i följande skärmbild.  ![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. Du kommer åt `Timeline` objektet i `MediaPlayer` med hjälp av `getTimeline()` metoden.

   Klassen `Timeline` kapslar in den information som är relaterad till innehållet på tidslinjen som är associerad med mediaobjektet som för närvarande läses in av `MediaPlayer` instansen. Klassen ger `Timeline` åtkomst till en skrivskyddad vy av den underliggande tidslinjen. Klassen innehåller en get-metod som ger en iterator genom en lista med `Timeline` `TimelineMarker` objekt.

1. Iterera genom listan med `TimelineMarkers` och använd den returnerade informationen för att implementera tidslinjen.

       Ett TimelineMarker-objekt innehåller två informationsdelar:
   
   * Markörens position på tidslinjen (i millisekunder)
   * Markörens varaktighet på tidslinjen (i millisekunder)

1. Lyssna efter `MediaPlayerEvent.TIMELINE_UPDATED` händelsen på `MediaPlayer` instansen och implementera `TimelineUpdatedEventListener.onTimelineUpdated()` återanropet.

   Objektet kan informera programmet om ändringar som kan inträffa på tidslinjen för uppspelning genom att anropa `Timeline` `OnTimelineUpdated` avlyssnaren.

```java
// access the timeline object 
Timeline timeline = mediaPlayer.getTimeline(); 
 
// Iterate through the list of TimelineMarkers 
Iterator<TimelineMarker> iterator = timeline.timelineMarkers(); 
 
while (iterator.hasNext()) { 
    TimelineMarker marker = iterator.next(); 
    // the start position of the marker 
    long startPos = marker.getTime(); 
    // the duration of the marker 
    long duration = marker.getDuration(); 
}
```
