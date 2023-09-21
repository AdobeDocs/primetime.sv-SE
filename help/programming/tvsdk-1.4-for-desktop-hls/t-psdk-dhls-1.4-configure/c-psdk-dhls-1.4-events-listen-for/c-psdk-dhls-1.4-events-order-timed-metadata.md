---
description: TVSDK skickar tidskodade metadatahändelser och genererar tidsbestämda metadata när standardtaggar eller anpassade taggar påträffas eller när en spellista ändras i ett manifest. Händelser skickas i den ordning som de visas i manifestet.
title: Händelser för tidsbestämda metadata
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Händelser för tidsbestämda metadata{#timed-metadata-events}

TVSDK skickar tidskodade metadatahändelser och genererar tidsbestämda metadata när standardtaggar eller anpassade taggar påträffas eller när en spellista ändras i ett manifest. Händelser skickas i den ordning som de visas i manifestet.

Spelaren implementerar åtgärder baserat på följande händelser:

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`: Skickas när tidsbestämda ID3-metadata bearbetas.
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`: Skickas när tidsbestämda metadata bearbetades och inga affärsmöjligheter identifierades.
