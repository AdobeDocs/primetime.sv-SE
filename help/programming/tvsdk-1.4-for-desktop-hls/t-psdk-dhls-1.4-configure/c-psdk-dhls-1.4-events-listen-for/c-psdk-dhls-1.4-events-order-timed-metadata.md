---
description: TVSDK skickar tidskodade metadatahändelser och genererar tidsbestämda metadata när standardtaggar eller anpassade taggar påträffas eller när en spellista ändras i ett manifest. Händelser skickas i den ordning som de visas i manifestet.
seo-description: TVSDK skickar tidskodade metadatahändelser och genererar tidsbestämda metadata när standardtaggar eller anpassade taggar påträffas eller när en spellista ändras i ett manifest. Händelser skickas i den ordning som de visas i manifestet.
seo-title: Händelser för tidsbestämda metadata
title: Händelser för tidsbestämda metadata
uuid: 69c43701-6ffa-45fe-a104-fe81391222e7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Händelser för tidsbestämda metadata{#timed-metadata-events}

TVSDK skickar tidskodade metadatahändelser och genererar tidsbestämda metadata när standardtaggar eller anpassade taggar påträffas eller när en spellista ändras i ett manifest. Händelser skickas i den ordning som de visas i manifestet.

Spelaren implementerar åtgärder baserat på följande händelser:

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`: Skickas när tidsbestämda ID3-metadata bearbetas.
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`: Skickas när tidsbestämda metadata bearbetades och inga affärsmöjligheter identifierades.

