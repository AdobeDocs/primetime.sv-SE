---
description: Direktinstallation förladdar delar av mediet på en eller flera kanaler. När en användare har valt eller bytt kanal börjar innehållet tidigare eftersom en del av bufferten redan har slutförts.
seo-description: Direktinstallation förladdar delar av mediet på en eller flera kanaler. När en användare har valt eller bytt kanal börjar innehållet tidigare eftersom en del av bufferten redan har slutförts.
seo-title: Direkt
title: Direkt
uuid: 98a5ef79-51e4-474e-a6e8-ca449c430b5e
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# Direkt {#instant-on}

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