---
description: Direktinstallation förladdar delar av mediet på en eller flera kanaler. När en användare har valt eller bytt kanal börjar innehållet tidigare eftersom en del av bufferten redan har slutförts.
title: Direkt
exl-id: 096104a7-867f-43e3-8433-f697d0224e21
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Direkt {#instant-on}

Direktinstallation förladdar delar av mediet på en eller flera kanaler. När en användare har valt eller bytt kanal börjar innehållet tidigare eftersom en del av bufferten redan har slutförts.

När spelaren finns i `PTMediaPlayerStatusReady` status, ring `prepareToPlay` om du vill läsa in och bearbeta en del av innehållet för senare uppspelning i förväg.

>[!TIP]
>
>Om du inte ringer `prepareToPlay`, ringa `play` anrop automatiskt `prepareToPlay` först. Förinläsningen och bearbetningen är klar.

TVSDK slutför några eller alla följande uppgifter för `prepareToPlay`:

* Om metadatanyckeln `kSyncCookiesWithAVAsset` är inställt gör TVSDK en begäran till den ursprungliga M3U8-filen om att synkronisera cookies.
* Läser in DRM-metadatanycklar.
* Skapar och förbereder vissa strukturer, element eller resurser som behövs för att spela upp innehåll.

>[!TIP]
>
>The `PTMediaPlayer` och `PTMediaPlayerItem` `prepareToPlay` är lika. Så här undviker du att skapa en separat `PTMediaPlayer` -instans för varje resurs använder du `PTMediaPlayerItem` -metod.

Med Direktstart kan du starta flera mediespelarinstanser, eller inläsarinstanser av mediespelarobjekt, samtidigt i bakgrunden och buffra videoströmmar i alla dessa instanser. När en användare ändrar kanalen och strömmen har buffrats korrekt, anropar `play` på den nya kanalen startar uppspelningen tidigare.
