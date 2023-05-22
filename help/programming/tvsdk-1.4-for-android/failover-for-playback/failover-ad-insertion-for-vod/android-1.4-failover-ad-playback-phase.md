---
description: TVSDK hämtar annonssegmenten och återger dem på enhetens skärm.
title: Ad-uppspelningsfas
exl-id: c12dcf84-0daa-4bc2-8e17-fdf47a760296
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Ad-uppspelningsfas{#ad-playback-phase}

TVSDK hämtar annonssegmenten och återger dem på enhetens skärm.

Nu har TVSDK löst annonser, placerat dem på tidslinjen och försökt återge innehållet på skärmen.

Följande huvudfelklasser kan förekomma i den här fasen:

* Fel vid anslutning till värdservern
* Fel vid hämtning av manifestfilen
* Fel vid hämtning av mediesegment

För alla tre felklasserna vidarebefordrar TVSDK utlösta händelser till ditt program, inklusive:

* Meddelandehändelser som utlöses när en redundans inträffar.
* Meddelandehändelser när profilen ändras på grund av redundansalgoritmen.
* Meddelandehändelser utlöses när alla alternativ för växling vid fel har beaktats och inga ytterligare åtgärder kan vidtas automatiskt.

   Programmet måste vidta rätt åtgärd.

Oavsett om fel inträffar eller inte anropar TVSDK onAdBreakComplete för varje `onAdBreakStart` och `onAdComplete` för varje `onAdStart`. Om segment inte kunde hämtas kan det dock finnas luckor i tidslinjen. När mellanrummen är tillräckligt stora kan värdena i spelhuvudet och den rapporterade annonsen visa avbrott.
