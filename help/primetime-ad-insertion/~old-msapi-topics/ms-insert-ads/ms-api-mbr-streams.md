---
description: Klientförfrågningar om annonsinfogning anger vanligtvis mer än en bithastighet i variantens M3U8-formaterade spelningslista. Manifestservern genererar och returnerar en ny variant av M3U8-fil som innehåller en separat M3U8-länk för varje bithastighet. Det genererar också ett unikt grupp-ID som knyter ihop dessa M3U8s.
seo-description: Klientförfrågningar om annonsinfogning anger vanligtvis mer än en bithastighet i variantens M3U8-formaterade spelningslista. Manifestservern genererar och returnerar en ny variant av M3U8-fil som innehåller en separat M3U8-länk för varje bithastighet. Det genererar också ett unikt grupp-ID som knyter ihop dessa M3U8s.
seo-title: Flera bithastighetsströmmar
title: Flera bithastighetsströmmar
uuid: f59cb765-e000-43e0-8d3a-8149a3c5b96e
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Flera bithastighetsströmmar {#multiple-bit-rate-streams}

Klientförfrågningar om annonsinfogning anger vanligtvis mer än en bithastighet i variantens M3U8-formaterade spelningslista. Manifestservern genererar och returnerar en ny variant av M3U8-fil som innehåller en separat M3U8-länk för varje bithastighet. Det genererar också ett unikt grupp-ID som knyter ihop dessa M3U8s.

Manifestservern använder informationen i klientens Bootstrap URL-begäran för att hämta innehållsvariantens spellista. Den genererar en ny variantspellista som innehåller manifestserverlänkar till innehåll på direktuppspelningsnivå. Klienten använder dessa för att konstruera förfrågningar om annonsinfogning. Manifestserverns innehållslänkar på flödesnivå har följande format:

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** Manifestservern anger det här värdet baserat på innehållets spellisttyp: Live/linear (#EXT-X-PLAYLIST-TYPE:EVENT) or VOD (#EXT-X-PLAYLIST-TYPE:VOD)

* **`publisherAssetID`** Utgivarens unika ID för det specifika innehåll som anges i Bootstrap URL-begäran.

* **`rendition`** Manifestservern anger detta baserat på BANDWIDTH-värdet för innehållsströmmen och använder det för att matcha bithastigheten för annonsen med bithastigheten för innehållet. Annonsbithastigheten får inte överskrida bithastigheten för innehållet om inte annonsåtergivningen med den lägsta bithastigheten gör det.

* **`groupID`** Manifestservern genererar det här värdet och använder det för att se till att annonserna placeras på ett konsekvent sätt, oavsett för vilken bithastighet som klienten begär annonser.

* **`base64-encoded url of the bit rate stream`** Manifestserverns URL-säkra base64 kodar innehållsströmmens absoluta URL. Varje ström har en egen URL.

* **`Query parameters`** Frågeparametrar finns i Bootstrap URL-begäran.

