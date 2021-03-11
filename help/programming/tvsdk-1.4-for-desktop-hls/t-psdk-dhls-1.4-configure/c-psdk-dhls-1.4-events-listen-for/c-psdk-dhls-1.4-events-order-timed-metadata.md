---
description: TVSDK skickar tidskodade metadatahändelser och genererar tidsbestämda metadata när standardtaggar eller anpassade taggar påträffas eller när en spellista ändras i ett manifest. Händelser skickas i den ordning som de visas i manifestet.
title: Händelser för tidsbestämda metadata
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# Tidsbestämda metadatahändelser{#timed-metadata-events}

TVSDK skickar tidskodade metadatahändelser och genererar tidsbestämda metadata när standardtaggar eller anpassade taggar påträffas eller när en spellista ändras i ett manifest. Händelser skickas i den ordning som de visas i manifestet.

Spelaren implementerar åtgärder baserat på följande händelser:

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`: Skickas när tidsbestämda ID3-metadata bearbetas.
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`: Skickas när tidsbestämda metadata bearbetades och inga affärsmöjligheter identifierades.

