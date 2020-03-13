---
description: Egenskapen MediaPlayerItem.timedMetadata ger dig åtkomst till alla TimedMetadata-objekt som skapats från taggarna playlist/manifest eller från ID3-taggar i medieströmmen. Egenskapen MediaPlayerItem.hasTimedMetadata anger om det finns en anpassad tagg som du prenumererar på i det aktuella mediet.
seo-description: Egenskapen MediaPlayerItem.timedMetadata ger dig åtkomst till alla TimedMetadata-objekt som skapats från taggarna playlist/manifest eller från ID3-taggar i medieströmmen. Egenskapen MediaPlayerItem.hasTimedMetadata anger om det finns en anpassad tagg som du prenumererar på i det aktuella mediet.
seo-title: Meddelanden om manifesttaggar
title: Meddelanden om manifesttaggar
uuid: 87bee41b-b44e-4d12-afd2-7a63023f992c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Meddelanden om manifesttaggar{#notifications-for-manifest-tags}

Egenskapen MediaPlayerItem.timedMetadata ger dig åtkomst till alla TimedMetadata-objekt som skapats från taggarna playlist/manifest eller från ID3-taggar i medieströmmen. Egenskapen MediaPlayerItem.hasTimedMetadata anger om det finns en anpassad tagg som du prenumererar på i det aktuella mediet.

Du kan övervaka tidsbestämda metadata genom att avlyssna följande händelser som meddelar programmet om relaterade aktiviteter:

* `MediaPlayerItemEvent.ITEM_CREATED`: Den inledande listan med `TimedMetadata` objekt är tillgänglig när `MediaPlayerItem` de har skapats. Den här händelsen meddelar programmet när detta händer.

* `MediaPlayerItemEvent.ITEM_UPDATED`: För live-/linjära strömmar där manifestet/spellistan uppdateras regelbundet kan ytterligare anpassade taggar visas i den uppdaterade spellistan/manifestet, så ytterligare TimedMetadata-objekt kan läggas till i `MediaPlayerItem.timedMetadata` egenskapen. Den här händelsen meddelar programmet när detta händer.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: Varje gång ett nytt `TimedMetadata` objekt skapas skickas den här händelsen av `MediaPlayer`. Den här händelsen skickas inte för det `TimedMetadata` objekt som skapades under initieringsfasen.

