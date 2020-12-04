---
description: TVSDK skickar händelser för annonsvisning som svar på tidsbestämda metadataåtgärder.
seo-description: TVSDK skickar händelser för annonsvisning som svar på tidsbestämda metadataåtgärder.
seo-title: Ad-servning/tidsbestämda metadatahändelser
title: Ad-servning/tidsbestämda metadatahändelser
uuid: fd50a937-0c9b-4c47-acb2-1ffc0592ad54
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Ad-servering/tidsbestämda metadatahändelser{#ad-serving-timed-metadata-events}

TVSDK skickar händelser för annonsvisning som svar på tidsbestämda metadataåtgärder.

Om du vill få meddelanden om alla sådana relaterade händelser registrerar du händelseavlyssnare med `MediaPlayer`-objektet för följande händelser.

| Händelse | Betydelse |
|---|---|
| TimedMetadataEvent.[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | En ID3-tidsmetadata bearbetades. |
| TimedMetadataEvent.[TIMED_METADATA_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | En tidsbestämd metadata bearbetades och ingen affärsmöjlighet identifierades. |
| TimedMetadataEvent.[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | Tidsbestämda metadata är tillgängliga och inga affärsmöjligheter identifierades. |
| TimedMetadataEvent.[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | Tidsbestämda metadata bearbetades och ingen affärsmöjlighet identifierades i bakgrundsmanifestet. |