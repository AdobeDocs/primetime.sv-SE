---
title: Använd Ad Insertion i Live-/Linear-ström
description: Använda Ad Insertion i Live-/Linear-ström
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Använd Ad Insertion i Live-/Linear-ström {#ad-insertion-live-linear-stream}

Primetime Ad Insertion ger utgivaren möjlighet att hantera vanliga och komplexa annonsinfogningssituationer som inträffar under live/linjära strömmar.

## Cue-format som stöds {#cue-formats-supported}

Primetime Ad Insertion har stöd för ett stort antal standardformat och icke-standardformat för cue, bland annat:

* DPI SCTE-35 (SCTE-35 förbättrad annonsmarkör)

* [Signalspecifikation för infogning av program i Adobe](https://www.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeDigitalProgramInsertionSignalingSpecification.pdf)

* Binary SCTE-35

Kontakta din supportrepresentant för Primetime om du vill ha mer information eller andra referenstyper som stöds.

## Stöd för partiell annonsbrytning {#partial-ad-break-support}

Delvisa annonsbrytningar kan användas i situationer där ett visningsprogram går in i en live/linjär ström efter att en annonsbrytning har startats.  Om ett visningsprogram till exempel anger en 2:00 lång annonsbrytning vid 1:00-markeringen säkerställer partiell infogning av annonsbrytningar att annonser kan visas under återstående tid. Utan partiell infogning av annonsradbrytningar skulle inga annonser skickas till den här läsaren under pausen. Primetime Ad Insertion aktiverar infogning av partiella annonsbrytningar som standard om det finns lämpliga taggar i medieströmmarna.

## Tidig avkastning (tidig annonsutträde) {#early-return-early-ad-exit}

Det finns tillfällen då det kan vara nödvändigt att gå tillbaka tidigt från en annonsbrytning i en live/linjär ström, till exempel när en sportevenemang plötsligt återgår till action. Varje annonsbeslutsformat innehåller taggen&quot;cue-out&quot; (ads) eller&quot;cue-in&quot; (innehåll). Om en&quot;cue-in&quot;-tagg påträffas före slutet av en annonsbrytning kommer Adobe Primetime Ad Insertion att respektera indata. Kontakta innehållspaketeraren för att aktivera tidig retur.
