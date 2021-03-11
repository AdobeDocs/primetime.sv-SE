---
description: Manifestservern stöder publiceringsaktiverade WebVTT-bildtexter för alla HLS-videoformat. När den tar emot förfrågningar om att infoga annonser i WebVTT-innehåll med bildtexter, är det korrekt.
title: Stöd för WebVTT-bildtexter
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# Stöd för WebVTT-bildtexter {#support-for-webvtt-captions}

Manifestservern stöder publiceringsaktiverade WebVTT-bildtexter för HLS-/DASH-videoformat. När den tar emot förfrågningar om att infoga annonser i WebVTT-innehåll med bildtexter, är det korrekt.

Om utgivaren inkluderar WebVTT-bildtexter i innehållet skickar manifestservern en innehållsström med bildtexter till klienten. WebVTT måste aktiveras av utgivaren för att manifestservern ska ha stöd för bildtexter. När klienten har WebVTT-bildtexter aktiverade och skickar en begäran till manifestservern ändrar manifestservern tidslinjen och WebVTT-spåret och returnerar innehåll med sammanslagna annonser och bildtexter till klienten.

Arbetsflödet för VOD-innehållsströmmar är följande:

1. Klienten skickar en innehållsström med WebVTT-bildtexter aktiverade till manifestservern.
1. Manifestservern manipulerar tidslinjen för att fästa annonser i innehållsströmmen.
1. Manifestservern ändrar WebVTT-spåret för att lägga till bildtexter till innehållet (inklusive annonser).
1. Manifestservern levererar innehållsströmmen till klienten, med infogade annonser och beskrivningar.

>[!NOTE]
>
>Om ett WebVTT-bildtextsegment finns i en annons från mitten av rullen ser användaren att bildtexten spelas upp före och efter den där annonsbrytningen. I ett 10 sekunder långt bildtextsegment med 30 sekunder lång och 5 sekunder lång annonsering ser användaren bildtextsegmentet under 5 sekunder före den mittre rullen och under 5 sekunder efter mittrullen.

>[!NOTE]
>
>Om en klient begär att en video ska spelas upp på ett specifikt språk, till exempel engelska, och sedan begär att videon ska spelas upp på franska, kan manifestservern inte identifiera att klienten har begärt att språket ska ändras till franska. Eftersom klienten inte kommunicerar med manifestservern infogar manifestservern annonsbeskrivningen i videoströmmen med det första språk som anges i annonsens M3U8 överordnad fil.
