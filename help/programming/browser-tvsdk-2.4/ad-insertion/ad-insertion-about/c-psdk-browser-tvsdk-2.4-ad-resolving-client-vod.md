---
description: För VOD-innehåll (video-on-demand) infogar Browser TVSDK annonsbrytningar genom att dela annonserna i huvudinnehållet så att tidslinjens varaktighet ökar.
title: VOD-annonsmatchning och infogning
exl-id: c2a2f14b-c90d-47fc-9dcc-eff8b1491dde
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# VOD-annonsmatchning och infogning{#vod-ad-resolving-and-insertion}

För VOD-innehåll (video-on-demand) infogar Browser TVSDK annonsbrytningar genom att dela annonserna i huvudinnehållet så att tidslinjens varaktighet ökar.

Före uppspelning löser Browser TVSDK kända annonser, infogar annonsbrytningar i huvudinnehållet enligt beskrivningen i en tidslinje som returneras från Adobe Primetime annonsbeslut och beräknar om den virtuella tidslinjen om det behövs.

Webbläsarens TVSDK infogar annonser på följande sätt:

* **Före rullning**, som är före innehållet.
* **Efterrullning**, som kommer efter innehållet.

När uppspelningen har startats kan inga ytterligare ändringar göras i innehållet. Ads cannot be:

* Infogad
* Borttagen

   Du kan t.ex. inte ta bort inbyggda annonser från innehållet för att erbjuda en reklamfri upplevelse.
* Ersatt

   Du kan till exempel inte ersätta inbyggda annonser med riktade annonser.
