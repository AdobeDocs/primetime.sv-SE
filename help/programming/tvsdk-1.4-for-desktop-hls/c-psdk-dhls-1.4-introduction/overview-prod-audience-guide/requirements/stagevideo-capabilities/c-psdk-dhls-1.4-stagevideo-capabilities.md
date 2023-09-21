---
description: På enheter som stöder GPU-acceleration (maskinvara) kan du använda ett flash.media.StageVideo-objekt för att bearbeta video på enhetens maskinvara. Tillgängligheten för StageVideo beror på vilka versioner och funktioner olika delar av systemet har, inklusive Flash Player, videomaskinvara, operativsystem, drivrutiner, webbläsare, nätverksanslutning och visningssammanhang.
title: StageVideo-funktioner och -begränsningar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Ökning {#stagevideo-capabilities-and-restrictions-overview}

På enheter som stöder GPU-acceleration (maskinvara) kan du använda ett flash.media.StageVideo-objekt för att bearbeta video på enhetens maskinvara. Tillgängligheten för StageVideo beror på vilka versioner och funktioner olika delar av systemet har, inklusive Flash Player, videomaskinvara, operativsystem, drivrutiner, webbläsare, nätverksanslutning och visningssammanhang.

The `StageVideo` kan du dra nytta av maskinvaruacceleration för att visa video på högsta möjliga prestandanivå för en enhet. Tillgänglighet och prestanda för `StageVideo` påverkas av följande faktorer:

* **Maskinvaruacceleration** - När maskinvaruacceleration är tillgänglig, `StageVideo` bearbetar video på enhetens maskinvara. När maskinvaruacceleration inte är tillgängligt `StageVideo` svarar beroende på vilken version av Flashen du kör:

   * *Flash 15 och senare* - När maskinvaruacceleration inte är tillgänglig, `StageVideo` använder programvara och du behöver inte göra något.

     >[!TIP]
     >
     >När maskinvaruacceleration inte är tillgängligt kan prestandan försämras avsevärt.

   * *Flash 14 och tidigare* - När maskinvaruacceleration inte är tillgänglig, `StageVideo` blir otillgänglig. I en liten uppsättning konfigurationer där maskinvaruacceleration inte stöds av webbläsaren eller grafikprocessorn, eller är inaktiverad i Flashen Player, kommer videouppspelning med TVSDK HLS-stacken att misslyckas. I *HDS* pipeline kan du växla från `StageVideo` till ett alternativ, till exempel Video-objektet, som bearbetar video i processorn.

* **Presentation** - Vid helskärmsvisning, `StageVideo` är alltid tillgängligt och prestanda ligger på den högsta nivå som är tillgänglig på enheten. Om du inte visar helskärmsläget används webbläsarens inställningar och funktioner för videopresentationen.

* **wmode** - I webbläsarsammanhang är `wmode` -inställningen är viktig för prestandan. Adobe rekommenderar att du behåller `wmode` ange till `direct` för att säkerställa bästa möjliga prestanda i webbläsarsammanhang.

  >[!NOTE]
  >
  >Kombinationen av faktorer som inkluderar `wmode`, `StageVideo`och Flash ger olika funktioner och begränsningar beroende på hur snabb maskinvaran är och vilken version av Flash du använder.

   * *Flash 15 och senare* - `StageVideo` är tillgänglig med alla tillgängliga `wmode` inställningar. Om du anger `wmode` till en annan inställning än `direct`, blir prestandan lägre.

   * *Flash 14 och tidigare* - Om du ställt in `wmode` till en annan inställning än `direct`, `StageVideo` är inte tillgängligt i alla webbläsare.
