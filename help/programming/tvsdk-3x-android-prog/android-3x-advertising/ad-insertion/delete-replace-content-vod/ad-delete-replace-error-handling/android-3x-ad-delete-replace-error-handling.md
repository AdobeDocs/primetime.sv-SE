---
description: TVSDK hanterar fel i tidsintervallet beroende på det specifika problemet genom att slå samman eller ändra ordning på de felaktigt definierade tidsintervallen.
seo-description: TVSDK hanterar fel i tidsintervallet beroende på det specifika problemet genom att slå samman eller ändra ordning på de felaktigt definierade tidsintervallen.
seo-title: Hantering av fel vid borttagning och ersättning av annonser
title: Hantering av fel vid borttagning och ersättning av annonser
uuid: 615f42b7-733a-49c4-bd7a-f14ad0d23fa0
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# Hantering av fel vid borttagning och ersättning av annonser {#ad-deletion-and-replacement-error-handling}

TVSDK hanterar fel i tidsintervallet beroende på det specifika problemet genom att slå samman eller ändra ordning på de felaktigt definierade tidsintervallen.

TVSDK hanterar `timeRanges` fel genom standardprocesser för sammanfogning och sortering. Först sorterar spelaren kunddefinierade tidsintervall efter *starttiden* . Baserat på den här sorteringsordningen sammanfogar TVSDK intilliggande intervall och sammanfogar dessa intervall om det finns delmängder och skärningar mellan intervallen.

TVSDK hanterar tidsintervallfel med följande alternativ:

* **Slut på ordning** : TVSDK ändrar ordning på tidsintervallen.

* **Delmängd** TVSDK sammanfogar deluppsättningar av tidsintervall.

* **Överlappa** TVSDK sammanfogar de överlappande tidsintervallen.

* **Om du ersätter intervall i konflikt** med TVSDK väljs ersättningstiden från den tidigaste `timeRange` som visas i gruppen i konflikt.

TVSDK hanterar signaleringslägeskonflikter med annonseringsmetadata på följande sätt:

* Om annonseringssignaleringsläget är i konflikt med tidsintervallets metadata har alltid tidsintervallets metadata prioritet.

   Om till exempel annonseringssignaleringsläget är inställt som servermappnings- eller manifestindikeringsalternativ, och det också finns MARK-tidsintervall i annonseringsmetadata, blir resultatet att intervallen markeras och inga annonser infogas.
* Om signeringsläget är inställt som cues för servermappning eller manifest för REPLACE-intervall, ersätts intervallen enligt vad som anges i REPLACE-intervallen, och det finns ingen annonsinfogning via servermappnings- eller manifest-cues.

   Mer information finns i tabellen *Signaleringsläge/Beteenden* för metadatakombination i [Effekt på infogning och borttagning av annonser i annonseringsläget](../../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/delete-replace-content-vod/android-3x-signaling-mode-android.md).

Kom ihåg följande:

* När servern inte returnerar giltig `AdBreaks`genererar och bearbetar TVSDK en `NOPTimelineOperation` för den tomma AdBreak och ingen annons spelas upp.

* Även om borttagning/ersättning av C3-annonser endast är avsedda att stödjas för VOD, om de anges i annonsens metadata, behandlas även tidsintervall för liveströmmar.
