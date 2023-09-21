---
description: Från Flash 15 och senare, när maskinvaruåtergivning med StageVideo inte är tillgängligt, återgår StageVideo sömlöst till ett StageVideo-programvaruobjekt.
title: Flash 15-stöd för StageVideo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# Flash 15-stöd för StageVideo{#flash-support-for-stagevideo}

Från Flash 15 och senare, när maskinvaruåtergivning med StageVideo inte är tillgängligt, återgår StageVideo sömlöst till ett StageVideo-programvaruobjekt.

Tänk på följande information om Flash 15 StageVideo som är en reserv till programmet:

* Inga kodändringar krävs i programmet.
* TVSDK behöver inte ändras.

  Du behöver ingen TVSDK-uppdatering för att kunna använda StageVideo-återgång till programvara.
* Programmen måste kompileras om för Flash 15.
* Program som du kompilerar om för Flash 15 fortsätter att fungera med Flash 14 och tidigare, så länge som dessa program inte använder några nya API:er som introducerades i Flash Player 15.

  Om Flash 14-programmet behöver använda ett nytt Flash 15-API måste du anropa API dynamiskt med en skiftning till objekttypen så att programmet inte misslyckas i Flash Player 14 vid körning.

## HTML-övertäckningar {#html-overlays}

I Flash 15 och senare kan du hantera en sömlös visning av HTML-övertäckningar när maskinvaruversionen av StageVideo blir otillgänglig och återgår till programvaran StageVideo. Aktivera den här funktionen genom att ange `wmode=opaque`.

Vissa äldre webbläsare stöder inte maskinvaruacceleration. Mer information om dessa krav finns i [Lägsta krav för StageVideo](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md). När du anger `wmode=opaque`, återges videon med StageVideo-programvaran som kan påverka prestanda. Vanligtvis, ange `wmode=direct` återger video direkt till GPU, vilket ger mycket bättre prestanda. Det här alternativet åsidosätter även övertäckningar för HTML.
