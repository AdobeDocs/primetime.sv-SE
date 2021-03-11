---
description: Egenskapen MediaPlayerItem.timedMetadata ger åtkomst till alla TimedMetadata-objekt som skapas från taggarna playlist/manifest eller från ID3-taggar i medieströmmen.
title: Meddelanden om manifesttaggar
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Meddelanden för manifesttaggar{#notifications-for-manifest-tags}

Egenskapen MediaPlayerItem.timedMetadata ger åtkomst till alla TimedMetadata-objekt som skapas från taggarna playlist/manifest eller från ID3-taggar i medieströmmen.

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

Egenskapen `MediaPlayerItem.hasTimedMetadata` anger om det finns en anpassad tagg som du prenumererar på i det aktuella mediet. Du kan övervaka tidsbestämda metadata genom att avlyssna `Events.TimedMetadataEvent`, som skickas av MediaPlayer-instansen varje gång ett nytt `TimedMetadata`-objekt skapas.
