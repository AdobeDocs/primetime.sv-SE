---
description: Egenskapen MediaPlayerItem.timedMetadata ger dig åtkomst till alla TimedMetadata-objekt som skapats från taggarna playlist/manifest eller från ID3-taggar i medieströmmen. Egenskapen MediaPlayerItem.hasTimedMetadata anger om det finns en anpassad tagg som du prenumererar på i det aktuella mediet.
title: Meddelanden om manifesttaggar
exl-id: 1a91fa47-edd5-4496-9755-17c906a3cf54
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
