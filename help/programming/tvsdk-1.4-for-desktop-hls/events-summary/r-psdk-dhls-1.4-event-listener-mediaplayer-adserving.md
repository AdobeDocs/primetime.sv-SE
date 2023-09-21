---
description: TVSDK skickar händelser för annonsvisning som svar på tidsbestämda metadataåtgärder.
title: Ad-servning/tidsbestämda metadatahändelser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# Ad-servning/tidsbestämda metadatahändelser{#ad-serving-timed-metadata-events}

TVSDK skickar händelser för annonsvisning som svar på tidsbestämda metadataåtgärder.

Om du vill få information om alla sådana relaterade händelser registrerar du händelseavlyssnare med `MediaPlayer` -objekt för följande händelser.

| Händelse | Betydelse |
|---|---|
| TimedMetadataEvent.[TIMETADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | En ID3-tidsmetadata bearbetades. |
| TimedMetadataEvent.[TIMED_METADATA_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | En tidsbestämd metadata bearbetades och ingen affärsmöjlighet identifierades. |
| TimedMetadataEvent.[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | Tidsbestämda metadata är tillgängliga och inga affärsmöjligheter identifierades. |
| TimedMetadataEvent.[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | Tidsbestämda metadata bearbetades och ingen affärsmöjlighet identifierades i bakgrundsmanifestet. |
