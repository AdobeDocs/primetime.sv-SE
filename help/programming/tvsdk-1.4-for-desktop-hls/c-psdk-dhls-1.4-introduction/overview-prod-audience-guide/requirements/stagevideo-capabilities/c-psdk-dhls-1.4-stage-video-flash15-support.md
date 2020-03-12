---
description: Från Flash 15 och senare, när maskinvaruåtergivning med StageVideo inte är tillgängligt, återgår StageVideo sömlöst till ett StageVideo-programvaruobjekt.
seo-description: Från Flash 15 och senare, när maskinvaruåtergivning med StageVideo inte är tillgängligt, återgår StageVideo sömlöst till ett StageVideo-programvaruobjekt.
seo-title: Flash 15-stöd för StageVideo
title: Flash 15-stöd för StageVideo
uuid: 49bd8703-016e-4fda-8773-5254d4774ec6
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184

---


# Flash 15-stöd för StageVideo{#flash-support-for-stagevideo}

Från Flash 15 och senare, när maskinvaruåtergivning med StageVideo inte är tillgängligt, återgår StageVideo sömlöst till ett StageVideo-programvaruobjekt.

Titta på följande information om Flash 15 StageVideo som återgår till programvara:

* Inga kodändringar krävs i programmet.
* TVSDK behöver inte ändras.

   Du behöver ingen TVSDK-uppdatering för att kunna använda StageVideo-återgång till programvara.
* Programmen måste kompileras om för Flash 15.
* Program som du kompilerar om för Flash 15 fortsätter att fungera med Flash 14 och tidigare, så länge som dessa program inte använder några nya API:er som introducerades i Flash Player 15.

   Om ditt Flash 14-program behöver använda ett nytt Flash 15-API måste du anropa API dynamiskt med en skiftning till objekttypen, så att programmet inte misslyckas i Flash Player 14 vid körning.

## HTML-övertäckningar {#html-overlays}

I Flash 15 och senare kan du hantera en sömlös visning av HTML-övertäckningar när maskinvaruversionen av StageVideo blir otillgänglig och återgår till programvaran StageVideo. Aktivera den här funktionen genom att ange `wmode=opaque`.

Vissa äldre webbläsare stöder inte maskinvaruacceleration. Mer information om de här kraven finns i [Lägsta krav](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md)för StageVideo. När du anger `wmode=opaque`det återges videon med programvaran StageVideo, som kan påverka prestandan. Vanligtvis återges video direkt i GPU-enheten när du anger `wmode=direct` det, vilket ger mycket bättre prestanda. Men det här alternativet åsidosätter även HTML-övertäckningar.
