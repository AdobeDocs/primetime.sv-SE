---
seo-title: Egenskaper för bevakad mapp
title: Egenskaper för bevakad mapp
uuid: fc204bb4-033a-46fe-8642-737f6a4cd1f1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Bevakade mappegenskaper {#watched-folder-properties}

Varje bevakad mapp innehåller en fil med namnet [!DNL properties/watchfolder.properties]. Den här filen innehåller paketeringsalternativen för innehåll som placeras i den här mappen, inklusive vad som ska krypteras och vilka profiler som ska användas. Ändringar som görs i värdena i egenskapsfilen börjar gälla nästa gång den bevakade mapppaketeraren körs (du behöver inte starta om servern).

Om det finns ett konfigurationsfel i paketerarens egenskapsfil stoppas paketerartråden. Starta om servern om du vill återuppta den bevakade mapppaketeraren. Om det finns ett konfigurationsfel i en bevakad mappegenskapsfil tas den bevakade mappen tillfälligt bort från listan med mappar som paketeraren bearbetar. Om du vill lägga till den bevakade mappen i listan igen startar du om servern eller ändrar paketeringsegenskapsfilen. Om ett fel inträffar under paketeringen av en viss fil (till exempel på grund av att filen är skadad) hoppas filen över och de återstående filerna i mappen bearbetas.
