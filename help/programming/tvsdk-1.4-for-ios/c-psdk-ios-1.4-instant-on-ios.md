---
description: Direktinstallation förladdar delar av mediet på en eller flera kanaler. När en användare har valt eller bytt kanal börjar innehållet tidigare eftersom en del av bufferten redan har slutförts.
title: Direkt
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Direkt{#instant-on}

Direktinstallation förladdar delar av mediet på en eller flera kanaler. När en användare har valt eller bytt kanal börjar innehållet tidigare eftersom en del av bufferten redan har slutförts.

När spelaren har statusen `PTMediaPlayerStatusReady` anropar du `prepareToPlay` för att ladda ned och bearbeta en del av innehållet för senare uppspelning.

>[!TIP]
>
>Om du inte anropar `prepareToPlay` anropar du `play` automatiskt `prepareToPlay` först. Förinläsningen och bearbetningen är klar.

TVSDK slutför några eller alla följande uppgifter för `prepareToPlay`:

* Om metadatanyckeln `kSyncCookiesWithAVAsset` är inställd gör TVSDK en begäran till den ursprungliga M3U8-filen om att synkronisera cookies.
* Läser in DRM-metadatanycklar.
* Skapar och förbereder vissa strukturer, element eller resurser som behövs för att spela upp innehåll.

>[!TIP]
>
>Metoderna `PTMediaPlayer` och `PTMediaPlayerItem` `prepareToPlay` är lika. Om du vill undvika att skapa en separat `PTMediaPlayer`-instans för varje resurs använder du metoden `PTMediaPlayerItem`.

Med Direktstart kan du starta flera mediespelarinstanser, eller inläsarinstanser av mediespelarobjekt, samtidigt i bakgrunden och buffra videoströmmar i alla dessa instanser. När en användare ändrar kanalen, och strömmen har buffrats korrekt, startar ett anrop till `play` på den nya kanalen uppspelningen tidigare.
