---
description: Från Flash 15 och senare, när maskinvaruåtergivning med StageVideo inte är tillgängligt, återgår StageVideo sömlöst till ett StageVideo-programvaruobjekt.
title: Flash 15-stöd för StageVideo
exl-id: 23ef0806-3aa5-4c48-a4f7-4ad9b72bdcc9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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

I Flash 15 och senare kan du hantera en sömlös visning av HTML-övertäckningar när maskinvaruversionen av StageVideo blir otillgänglig och återgår till programvaran StageVideo. Aktivera den här funktionen genom att ange `wmode=opaque`.

Vissa äldre webbläsare stöder inte maskinvaruacceleration. Mer information om dessa krav finns i [Lägsta krav för StageVideo](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md). När du anger `wmode=opaque`, återges videon med StageVideo-programvaran som kan påverka prestanda. Vanligtvis, ange `wmode=direct` återger video direkt till GPU, vilket ger mycket bättre prestanda. Det här alternativet åsidosätter även övertäckningar för HTML.
