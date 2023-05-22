---
title: Egenskaper för bevakad mapp
description: Egenskaper för bevakad mapp
copied-description: true
exl-id: e86518d4-2a16-45c7-aa96-189f677c3ee6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Egenskaper för bevakad mapp {#watched-folder-properties}

Varje bevakad mapp innehåller en fil som heter [!DNL properties/watchfolder.properties]. Den här filen innehåller paketeringsalternativen för innehåll som placeras i den här mappen, inklusive vad som ska krypteras och vilka profiler som ska användas. Ändringar som görs i värdena i egenskapsfilen börjar gälla nästa gång den bevakade mapppaketeraren körs (du behöver inte starta om servern).

Om det finns ett konfigurationsfel i paketerarens egenskapsfil stoppas paketerartråden. Starta om servern om du vill återuppta den bevakade mapppaketeraren. Om det finns ett konfigurationsfel i en bevakad mappegenskapsfil tas den bevakade mappen tillfälligt bort från listan med mappar som paketeraren bearbetar. Om du vill lägga till den bevakade mappen i listan igen startar du om servern eller ändrar paketeringsegenskapsfilen. Om ett fel inträffar under paketeringen av en viss fil (till exempel på grund av att filen är skadad) hoppas filen över och de återstående filerna i mappen bearbetas.
