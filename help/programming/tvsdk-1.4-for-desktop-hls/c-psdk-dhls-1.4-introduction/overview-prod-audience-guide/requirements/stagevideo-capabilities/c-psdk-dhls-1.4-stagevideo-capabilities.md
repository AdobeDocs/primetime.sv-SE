---
description: På enheter som stöder GPU-acceleration (maskinvara) kan du använda ett flash.media.StageVideo-objekt för att bearbeta video på enhetens maskinvara. Tillgängligheten för StageVideo beror på vilka versioner och funktioner olika delar av systemet har, inklusive Flash Player, videomaskinvara, operativsystem, drivrutiner, webbläsare, nätverksanslutning och visningssammanhang.
seo-description: På enheter som stöder GPU-acceleration (maskinvara) kan du använda ett flash.media.StageVideo-objekt för att bearbeta video på enhetens maskinvara. Tillgängligheten för StageVideo beror på vilka versioner och funktioner olika delar av systemet har, inklusive Flash Player, videomaskinvara, operativsystem, drivrutiner, webbläsare, nätverksanslutning och visningssammanhang.
seo-title: StageVideo-funktioner och -begränsningar
title: StageVideo-funktioner och -begränsningar
uuid: 7556f30b-4b9f-4258-beb6-2a4ce8f05d1a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Översikt {#stagevideo-capabilities-and-restrictions-overview}

På enheter som stöder GPU-acceleration (maskinvara) kan du använda ett flash.media.StageVideo-objekt för att bearbeta video på enhetens maskinvara. Tillgängligheten för StageVideo beror på vilka versioner och funktioner olika delar av systemet har, inklusive Flash Player, videomaskinvara, operativsystem, drivrutiner, webbläsare, nätverksanslutning och visningssammanhang.

Med klassen `StageVideo` kan du dra nytta av maskinvaruacceleration för att visa video på högsta möjliga prestandanivå för en enhet. Tillgängligheten och prestandan för `StageVideo` påverkas av följande faktorer:

* **Maskinvaruacceleration**  - När maskinvaruacceleration är tillgänglig  `StageVideo` bearbetas video på enhetens maskinvara. När maskinvaruacceleration inte är tillgängligt beror `StageVideo`-svaren på vilken version av Flash du kör:

   * *Flash 15 och senare*  - När maskinvaruacceleration inte är tillgänglig  `StageVideo` återgår du till programvara och behöver inte göra något.

      >[!TIP]
      >
      >När maskinvaruacceleration inte är tillgängligt kan prestandan försämras avsevärt.

   * *Flash 14 och tidigare*  - När maskinvaruacceleration inte är tillgänglig  `StageVideo` blir den otillgänglig. I en liten uppsättning konfigurationer där maskinvaruacceleration inte stöds av webbläsaren eller grafikprocessorn, eller är avstängd i Flash Player, kommer videouppspelning med TVSDK HLS-stacken att misslyckas. I *HDS*-pipelinen kan du växla från `StageVideo` till ett alternativ, till exempel Video-objektet, som bearbetar video i CPU:n.

* **Presentationskontext**  - Under helskärmsvisning  `StageVideo` är alltid tillgängligt och prestanda är på den högsta tillgängliga nivån på enheten. Om du inte visar helskärmsläget används webbläsarens inställningar och funktioner för videopresentationen.

* **wmode**  - I webbläsarsammanhang är  `wmode` inställningen viktig för prestandan. Adobe rekommenderar att du behåller `wmode` inställt på `direct` för att få bästa möjliga prestanda i webbläsarkontexten.

   >[!NOTE]
   >
   >Kombinationen av faktorer som inkluderar `wmode`, `StageVideo` och Flash ger olika funktioner och begränsningar beroende på hur snabb maskinvaran är och vilken version av Flash du använder.

   * *Flash 15 och senare*  -  `StageVideo` finns med alla tillgängliga  `wmode` inställningar. Om du ställer in `wmode` på en annan inställning än `direct`, blir dock prestandan lägre.

   * *Flash 14 och tidigare*  - Om du anger  `wmode` en annan inställning än  `direct`är den inte  `StageVideo` tillgänglig i alla webbläsare.

