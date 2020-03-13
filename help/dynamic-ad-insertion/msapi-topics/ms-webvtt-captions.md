---
description: Manifestservern stöder publiceringsaktiverade WebVTT-bildtexter för alla HLS-videoformat. När den tar emot förfrågningar om att infoga annonser i WebVTT-innehåll med bildtexter, är det korrekt.
seo-description: Manifestservern stöder publiceringsaktiverade WebVTT-bildtexter för alla HLS-videoformat. När den tar emot förfrågningar om att infoga annonser i WebVTT-innehåll med bildtexter, är det korrekt.
seo-title: Stöd för WebVTT-bildtexter
title: Stöd för WebVTT-bildtexter
uuid: 1dc728b0-5aeb-4c48-8f3b-54ff4b135742
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Stöd för WebVTT-bildtexter {#support-for-webvtt-captions}

Manifestservern stöder publiceringsaktiverade WebVTT-bildtexter för alla HLS-videoformat. När den tar emot förfrågningar om att infoga annonser i WebVTT-innehåll med bildtexter, är det korrekt.

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
>Om en klient begär att en video ska spelas upp på ett specifikt språk, till exempel engelska, och sedan begär att videon ska spelas upp på franska, kan manifestservern inte identifiera att klienten har begärt att språket ska ändras till franska. Eftersom klienten inte kommunicerar med manifestservern infogar manifestservern annonsbeskrivningen i videoströmmen med det första språk som anges i annonsens M3U8-huvudfil.