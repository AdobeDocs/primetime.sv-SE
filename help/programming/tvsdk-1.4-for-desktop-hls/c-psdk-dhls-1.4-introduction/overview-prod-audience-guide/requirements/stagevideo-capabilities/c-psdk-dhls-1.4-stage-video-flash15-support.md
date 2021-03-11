---
description: Från Flash 15 och senare, när maskinvaruåtergivning med StageVideo inte är tillgängligt, återgår StageVideo sömlöst till ett StageVideo-programvaruobjekt.
title: Flash 15-stöd för StageVideo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Flash 15-stöd för StageVideo{#flash-support-for-stagevideo}

Från Flash 15 och senare, när maskinvaruåtergivning med StageVideo inte är tillgängligt, återgår StageVideo sömlöst till ett StageVideo-programvaruobjekt.

Titta på följande information om StageVideo-återgång till programmet Flash 15:

* Inga kodändringar krävs i programmet.
* TVSDK behöver inte ändras.

   Du behöver ingen TVSDK-uppdatering för att kunna använda StageVideo-återgång till programvara.
* Programmen måste kompileras om för Flash 15.
* Program som du kompilerar om för Flash 15 fortsätter att fungera med Flash 14 och tidigare, så länge som dessa program inte använder några nya API:er som introducerades i Flash Player 15.

   Om ditt Flash 14-program behöver använda ett nytt Flash 15-API måste du anropa API dynamiskt med en skiftning till objekttypen så att programmet inte misslyckas i Flash Player 14 vid körning.

## HTML-övertäckningar {#html-overlays}

I Flash 15 och senare kan du hantera en sömlös visning av HTML-övertäckningar när maskinvaruversionen av StageVideo blir otillgänglig och återgår till programvaran StageVideo. Om du vill aktivera den här funktionen anger du `wmode=opaque`.

Vissa äldre webbläsare stöder inte maskinvaruacceleration. Mer information om dessa krav finns i [Lägsta krav för StageVideo](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md). När du anger `wmode=opaque` återges videon med programvaran StageVideo, som kan påverka prestanda. Om du ställer in `wmode=direct` återges videon direkt till GPU, vilket ger mycket bättre prestanda. Men det här alternativet åsidosätter även HTML-övertäckningar.
