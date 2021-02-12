---
title: Kom igång med Adobe Primetime Ad Insertion
description: Komma igång med Adobe Primetime Ad Insertion
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# Kom igång med Adobe Primetime Ad Insertion {#ptai-get-started}

Primetime Ad Insertion samordnar de system som tillhandahåller innehåll och annonser för att skapa personaliserade annonsupplevelser i strömmen och spårar sedan annonsuppspelningen för era annonsörer.

Primetime Ad Insertion interagerar med klientapplikationer för videoleverans genom att skriva om videomanifest för att tillhandahålla riktade annonser och personaliserade upplevelser för varje visningsprogram. De här manifesten kombinerar innehåll och annonser som levereras från en annonsserver och kan även innehålla metadata med detaljerade anvisningar för annonsspårning. Primetime Ad Insertion har stöd för annonsspårning både på klientsidan och serversidan.

När systemet har konfigurerats korrekt kan ett typiskt arbetsflöde se ut så här:

1. Klientprogrammet genererar en [Bootstrap-URL](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) med information om videoströmmen och skickar en GET-begäran till Primetime Ad Insertion.  Primetime Ad Insertion stöder HLS och DASH med en mängd olika annonssignalformat.

1. Primetime Ad Insertion svarar genom att skicka innehållsmanifestet från utgivarens CDN tillbaka till klientprogrammet.

1. Klientprogrammet väljer lämpliga strömmar i det genererade manifestet som ska spelas upp och skickar begäranden till Primetime Ad Insertion.

1. Primetime Ad Insertion hämtar de begärda strömmarna från CDN-innehållet, tolkar/läser eventuell referensuppgifter, anropar annonsservern och ersätter annonsbrytningar efter behov.

1. Primetime Ad Insertion normaliserar manifestet genom att skriva om resurs-URL:er och identifiera om annonskreatörer behöver omkodning, se [Ad Transcoding](/help/primetime-ad-insertion/just-in-time-transcoding/jit-transcoding-overview.md) just-in-time.

1. Primetime Ad Insertion hämtar de annonskreatörer som behövs och infogar lämpliga fragment i manifesten.

1. Primetime Ad Insertion levererar de färdiga stygna manifesten, inklusive annonser, till klientprogrammet för uppspelning.

1. Annonsleverans och visningsbarhet kan mätas antingen via klient- eller serverannonsspårning, se [Konfigurera annonsspårning](/help/primetime-ad-insertion/getting-started/set-up-ad-tracking.md).

Primetime Ad Insertion stöder de flesta HLS/DASH-klient- och spelarkonfigurationer. Mer information om vilka specifika annonssigneringsformat som stöds finns i [Cue-format](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md) som stöds.
