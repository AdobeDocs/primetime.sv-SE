---
description: TVSDK hämtar annonssegmenten och återger dem på enhetens skärm.
title: Ad-uppspelningsfas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Ad-playback phase{#ad-playback-phase}

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

Oavsett om fel inträffar eller inte anropar TVSDK onAdBreakComplete för var `onAdBreakStart` och `onAdComplete` för var `onAdStart`. Om segment inte kunde hämtas kan det dock finnas luckor i tidslinjen. När mellanrummen är tillräckligt stora kan värdena i spelhuvudet och den rapporterade annonsen visa avbrott.
