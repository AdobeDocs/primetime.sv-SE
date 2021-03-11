---
description: TVSDK hanterar fel i tidsintervallet beroende på det specifika problemet genom att slå samman eller ändra ordning på de felaktigt definierade tidsintervallen.
title: Hantering av fel vid borttagning och ersättning av annonser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Översikt {#ad-deletion-and-replacement-error-handling-overview}

TVSDK hanterar fel i tidsintervallet beroende på det specifika problemet genom att slå samman eller ändra ordning på de felaktigt definierade tidsintervallen.

TVSDK hanterar `timeRanges` fel genom standardprocesser för sammanfogning och sortering. Först sorterar spelaren kunddefinierade tidsintervall efter *början*. Baserat på den här sorteringsordningen sammanfogar TVSDK intilliggande intervall och sammanfogar dessa intervall om det finns delmängder och skärningar mellan intervallen.

TVSDK hanterar tidsintervallfel med följande alternativ:

* **Slut på** ordningTVSDK ordnar om tidsintervallen.

* **** SubsetTVSDK sammanfogar delmängder av tidsintervall.

* **Intersect** TVSDK sammanfogar de överlappande tidsintervallen.

* **Ersätt intervall i** konfliktTVSDK väljer ersättningstiden från den tidigaste  `timeRange` som visas i gruppen i konflikt.

TVSDK hanterar signaleringslägeskonflikter med annonseringsmetadata på följande sätt:

* Om annonseringssignaleringsläget är i konflikt med tidsintervallets metadata har alltid tidsintervallets metadata prioritet.

   Om till exempel annonseringssignaleringsläget är inställt som servermappnings- eller manifestindikeringsalternativ, och det också finns MARK-tidsintervall i annonseringsmetadata, blir resultatet att intervallen markeras och inga annonser infogas.
* Om signeringsläget är inställt som cues för servermappning eller manifest för REPLACE-intervall, ersätts intervallen enligt vad som anges i REPLACE-intervallen, och det finns ingen annonsinfogning via servermappnings- eller manifest-cues.

   Mer information finns i tabellen *Signaleringsläge / Metadatakombinationsbeteenden* i [Effekt på annonsinfogning och borttagning från annonseringsläge..](../../../../tvsdk-2.7-for-android/ad-insertion/delete-replace-content-vod/c-psdk-android-2.7-signaling-mode-metadata-combos-android.md#c_psdk_signaling-mode-metadata-combos-android).

Kom ihåg följande:

* När servern inte returnerar giltig `AdBreaks` genererar och bearbetar TVSDK en `NOPTimelineOperation` för den tomma AdBreak och ingen annons spelas upp.

* Även om borttagning/ersättning av C3-annonser endast är avsedda att stödjas för VOD, om de anges i annonsens metadata, behandlas även tidsintervall för liveströmmar.

