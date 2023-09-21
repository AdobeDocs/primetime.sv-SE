---
description: Egenskapen MediaPlayerItem.timedMetadata ger åtkomst till alla TimedMetadata-objekt som skapas från taggarna playlist/manifest eller från ID3-taggar i medieströmmen.
title: Meddelanden om manifesttaggar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Meddelanden om manifesttaggar{#notifications-for-manifest-tags}

Egenskapen MediaPlayerItem.timedMetadata ger åtkomst till alla TimedMetadata-objekt som skapas från taggarna playlist/manifest eller från ID3-taggar i medieströmmen.

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

The `MediaPlayerItem.hasTimedMetadata` anger om det finns en anpassad tagg som du prenumererar på i det aktuella mediet. Du kan övervaka tidsbestämda metadata genom att avlyssna `Events.TimedMetadataEvent`som MediaPlayer-instansen skickar varje gång en ny `TimedMetadata` objektet skapas.
