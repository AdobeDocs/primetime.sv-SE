---
title: Kom igång med Adobe Primetime Ad Insertion
description: Komma igång med Adobe Primetime Ad Insertion
translation-type: tm+mt
source-git-commit: 2a9bb089cda2b315f91b30d5cab0db9b3e372799
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# Kom igång med Adobe Primetime Ad Insertion {#ptai-get-started}

Primetime Ad Insertion samordnar de system som tillhandahåller innehåll och annonser för att skapa personaliserade annonsupplevelser i strömmen och spårar sedan annonsuppspelningen för era annonsörer.

Primetime Ad Insertion interagerar med klientapplikationer för videoleverans genom att skriva om videomanifest för att tillhandahålla riktade annonser och personaliserade upplevelser för varje visningsprogram. De här manifesten kombinerar innehåll och annonser som levereras från en annonsserver och kan även innehålla metadata med detaljerade anvisningar för annonsspårning. Primetime Ad Insertion har stöd för annonsspårning både på klientsidan och serversidan.

När systemet har konfigurerats korrekt kan ett typiskt arbetsflöde se ut så här:

1. Klientprogrammet genererar en [Bootstrap-URL](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md) med information om videoströmmen och skickar en GET-begäran till Primetime Ad Insertion.

1. Primetime Ad Insertion svarar genom att skicka innehållsmanifestet från utgivarens CDN tillbaka till klientprogrammet.

1. Klientprogrammet väljer lämpliga strömmar i det genererade manifestet som ska spelas upp och skickar begäranden till Primetime Ad Insertion.

1. Primetime Ad Insertion hämtar de begärda strömmarna från CDN-innehållet, tolkar/läser eventuell referensuppgifter, anropar annonsservern och ersätter annonsbrytningar efter behov.

1. Primetime Ad Insertion normaliserar manifestet genom att skriva om resurs-URL:er och identifiera om annonskreatörer behöver omkodning. <!-- see [Just-in-time ad transcoding](just-in-time-transcoding.md) and [packaging](just-in-time-repackaging.md).-->

1. Primetime Ad Insertion hämtar de annonskreatörer som behövs och infogar lämpliga fragment i manifesten.

1. Primetime Ad Insertion levererar de färdiga stygna manifesten, inklusive annonser, till klientprogrammet för uppspelning.

1. Annonsleverans och visningsbarhet kan mätas antingen via klient- eller serversidesannonsspårning, se [Konfigurera annonsspårning](set-up-ad-tracking.md).

Primetime Ad Insertion stöder de flesta klientkonfigurationer för HLS/DASH.
