---
description: Tidslinjen för annonsen som är lämplig för en uppspelning av VOD-innehåll kan vara olämplig för efterföljande uppspelningar. Du kan ersätta en VOD-tidslinje utan att ändra innehållet.
seo-description: Tidslinjen för annonsen som är lämplig för en uppspelning av VOD-innehåll kan vara olämplig för efterföljande uppspelningar. Du kan ersätta en VOD-tidslinje utan att ändra innehållet.
seo-title: Ändringar i VOD
title: Ändringar i VOD
uuid: e734aacd-b42e-4c8e-a16a-c7a0739a0492
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Ändringar i VOD {#changes-to-vod}

Tidslinjen för annonsen som är lämplig för en uppspelning av VOD-innehåll kan vara olämplig för efterföljande uppspelningar. Du kan ersätta en VOD-tidslinje utan att ändra innehållet.

Exempel på situationer där du kan vilja ersätta en VOD-tidslinje är:

* Ersätt lokala annonser, men lämna nationella annonser under ett C3-fönster.
* Ersätt inbrända annonser när C3-fönstret stängs.
* Ersätt dynamiskt gamla C3-annonser med nyare annonser med längre varaktighet.
* Infoga färre annonser eller inga alls.

Du kan ersätta annonstidslinjen genom att skicka en ny annonsinsättningsbegäran med den ursprungliga M3U8-filen och ett annat värde för frågeparametern `pttimeline`.