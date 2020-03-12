---
description: För VOD-innehåll (video-on-demand) infogar TVSDK annonsbrytningar genom att dela annonserna i huvudinnehållet så att tidslinjens varaktighet ökar.
seo-description: För VOD-innehåll (video-on-demand) infogar TVSDK annonsbrytningar genom att dela annonserna i huvudinnehållet så att tidslinjens varaktighet ökar.
seo-title: Lös och infoga VOD-annons
title: Lös och infoga VOD-annons
uuid: b7124cab-441b-4b38-ac83-300ab9e5f9ec
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Lös och infoga VOD-annonser {#resolve-and-insert-vod-ad}

För VOD-innehåll (video-on-demand) infogar TVSDK annonsbrytningar genom att dela annonserna i huvudinnehållet så att tidslinjens varaktighet ökar.

Före uppspelning löser TVSDK kända annonser, infogar annonsbrytningar i huvudinnehållet enligt beskrivningen i en tidslinje som returneras från Adobe Primetime-annonsbeslut och beräknar om den virtuella tidslinjen om det behövs.

TVSDK infogar annonser på följande sätt:

* **Pre-roll**, som placeras före innehållet.
* **Mid-roll**, som är mitt i innehållet.
* **Efterrullning**, som placeras efter innehållet.

>[!TIP]
>
>När uppspelningen har startats kan inga ytterligare ändringar göras i innehållet.

Ads cannot be:

* Infogad
* Borttagen

   Du kan t.ex. inte ta bort inbyggda annonser från innehållet för att erbjuda en reklamfri upplevelse.
* Ersatt

   Du kan till exempel inte ersätta inbyggda annonser med riktade annonser.