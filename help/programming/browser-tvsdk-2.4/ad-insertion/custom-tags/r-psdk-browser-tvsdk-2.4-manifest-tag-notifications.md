---
description: Egenskapen MediaPlayerItem.timedMetadata ger åtkomst till alla TimedMetadata-objekt som skapas från taggarna playlist/manifest eller från ID3-taggar i medieströmmen.
seo-description: Egenskapen MediaPlayerItem.timedMetadata ger åtkomst till alla TimedMetadata-objekt som skapas från taggarna playlist/manifest eller från ID3-taggar i medieströmmen.
seo-title: Meddelanden om manifesttaggar
title: Meddelanden om manifesttaggar
uuid: 50727455-b37b-4e39-8efb-a97de3164074
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Meddelanden om manifesttaggar{#notifications-for-manifest-tags}

Egenskapen MediaPlayerItem.timedMetadata ger åtkomst till alla TimedMetadata-objekt som skapas från taggarna playlist/manifest eller från ID3-taggar i medieströmmen.

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

Egenskapen anger `MediaPlayerItem.hasTimedMetadata` om det finns en anpassad tagg som du prenumererar på i det aktuella mediet. Du kan övervaka tidsbestämda metadata genom att avlyssna `Events.TimedMetadataEvent`, som skickas av MediaPlayer-instansen varje gång ett nytt `TimedMetadata` objekt skapas.
