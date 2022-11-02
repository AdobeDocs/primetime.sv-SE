---
description: Du kan få en beskrivning av tidslinjen som är associerad med det markerade objekt som spelas upp av TVSDK. Detta är mest användbart när programmet visar en anpassad navigeringsfältskontroll där innehållsavsnitt som motsvarar annonsinnehåll identifieras.
title: Inspect tidslinjen för uppspelning
exl-id: af373f1e-ed5b-40a9-a91e-9eb0e4a181de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Inspect tidslinjen för uppspelning{#inspect-the-playback-timeline}

Du kan få en beskrivning av tidslinjen som är associerad med det markerade objekt som spelas upp av TVSDK. Detta är mest användbart när programmet visar en anpassad navigeringsfältskontroll där innehållsavsnitt som motsvarar annonsinnehåll identifieras.

Här är ett exempel på implementering som visas i följande skärmbild.  ![](assets/inspect-playback.jpg){width="368.641pt"}

1. Öppna `Timeline` objekt i `MediaPlayer` med `getTimeline` -metod.

   The `Timeline` klassen kapslar in informationen som är relaterad till innehållet på tidslinjen som är associerad med mediaobjektet som för närvarande är inläst av `MediaPlayer` -instans. The `Timeline` -klassen ger åtkomst till en skrivskyddad vy av den underliggande tidslinjen. The `Timeline` klassen innehåller en get-metod som ger en iterator via en lista med `TimelineMarker` objekt.

1. Upprepa i listan `TimelineMarkers` och använd den returnerade informationen för att implementera tidslinjen.

       Ett TimelineMarker-objekt innehåller två informationsdelar:
   
   * Markörens position på tidslinjen (i millisekunder)
   * Markörens varaktighet på tidslinjen (i millisekunder)

1. Implementera gränssnittet för avlyssnaråteranrop `MediaPlayer.PlaybackEventListener.onTimelineUpdated` och registrera det med `Timeline` -objekt.

   The `Timeline` -objektet kan informera programmet om ändringar som kan inträffa på tidslinjen genom att anropa `OnTimelineUpdated` avlyssnare.

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
