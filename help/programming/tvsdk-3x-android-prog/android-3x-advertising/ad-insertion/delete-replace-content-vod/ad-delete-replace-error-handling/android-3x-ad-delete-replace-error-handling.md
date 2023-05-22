---
description: TVSDK hanterar fel i tidsintervallet beroende på det specifika problemet genom att slå samman eller ändra ordning på de felaktigt definierade tidsintervallen.
title: Hantering av fel vid borttagning och ersättning av annonser
exl-id: 40d1cf67-df8c-4c5f-a1f2-defe3dd2b44a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Hantering av fel vid borttagning och ersättning av annonser  {#ad-deletion-and-replacement-error-handling}

TVSDK hanterar fel i tidsintervallet beroende på det specifika problemet genom att slå samman eller ändra ordning på de felaktigt definierade tidsintervallen.

TVSDK hanterar `timeRanges` fel genom standardprocesser för sammanfogning och sortering. Först sorterar spelaren kunddefinierade tidsintervall efter *begin* tid. Baserat på den här sorteringsordningen sammanfogar TVSDK intilliggande intervall och sammanfogar dessa intervall om det finns delmängder och skärningar mellan intervallen.

TVSDK hanterar tidsintervallfel med följande alternativ:

* **Oordning** TVSDK ändrar ordning på tidsintervallen.

* **Delmängd** TVSDK sammanfogar delmängder av tidsintervall.

* **Överlappa** TVSDK sammanfogar de överlappande tidsintervallen.

* **Ersätt intervallkonflikt** TVSDK väljer ersättningens varaktighet från det tidigaste `timeRange` som visas i den grupp som står i konflikt.

TVSDK hanterar signaleringslägeskonflikter med annonseringsmetadata på följande sätt:

* Om annonseringssignaleringsläget är i konflikt med tidsintervallets metadata har alltid tidsintervallets metadata prioritet.

   Om till exempel annonseringssignaleringsläget är inställt som servermappnings- eller manifestindikeringsalternativ, och det också finns MARK-tidsintervall i annonseringsmetadata, blir resultatet att intervallen markeras och inga annonser infogas.
* Om signeringsläget är inställt som cues för servermappning eller manifest för REPLACE-intervall, ersätts intervallen enligt vad som anges i REPLACE-intervallen, och det finns ingen annonsinfogning via servermappnings- eller manifest-cues.

   Mer information finns i *Signeringsläge/Metadatakombinationsbeteenden* tabell i [Effekt vid infogning och borttagning av annonser i signeringsläge](../../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/delete-replace-content-vod/android-3x-signaling-mode-android.md).

Kom ihåg följande:

* När servern inte returnerar giltig `AdBreaks`, TVSDK genererar och bearbetar en `NOPTimelineOperation` för den tomma AdBreak, och ingen annons spelas upp.

* Även om borttagning/ersättning av C3-annonser endast är avsedda att stödjas för VOD, om de anges i annonsens metadata, behandlas även tidsintervall för liveströmmar.
