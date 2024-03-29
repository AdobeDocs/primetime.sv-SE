---
description: Egenskapen MediaPlayerItem.timedMetadata ger dig åtkomst till alla TimedMetadata-objekt som skapats från taggarna playlist/manifest eller från ID3-taggar i medieströmmen. Egenskapen MediaPlayerItem.hasTimedMetadata anger om det finns en anpassad tagg som du prenumererar på i det aktuella mediet.
title: Meddelanden om manifesttaggar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Meddelanden om manifesttaggar{#notifications-for-manifest-tags}

Egenskapen MediaPlayerItem.timedMetadata ger dig åtkomst till alla TimedMetadata-objekt som skapats från taggarna playlist/manifest eller från ID3-taggar i medieströmmen. Egenskapen MediaPlayerItem.hasTimedMetadata anger om det finns en anpassad tagg som du prenumererar på i det aktuella mediet.

Du kan övervaka tidsbestämda metadata genom att avlyssna följande händelser som meddelar programmet om relaterade aktiviteter:

* `MediaPlayerItemEvent.ITEM_CREATED`: Den inledande listan med `TimedMetadata` objekt är tillgängliga efter `MediaPlayerItem` skapas. Den här händelsen meddelar programmet när detta händer.

* `MediaPlayerItemEvent.ITEM_UPDATED`: För live-/linjära strömmar där manifestet/spellistan uppdateras regelbundet kan ytterligare anpassade taggar visas i den uppdaterade spellistan/manifestet, så ytterligare TimedMetadata-objekt kan läggas till i `MediaPlayerItem.timedMetadata` -egenskap. Den här händelsen meddelar programmet när detta händer.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: Varje gång en ny `TimedMetadata` objektet skapas, den här händelsen skickas av `MediaPlayer`. Den här händelsen skickas inte för `TimedMetadata` objekt som skapades under initieringsfasen.
