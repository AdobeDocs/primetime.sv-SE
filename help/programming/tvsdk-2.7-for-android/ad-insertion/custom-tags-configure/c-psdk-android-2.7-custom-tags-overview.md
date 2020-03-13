---
seo-title: Exempel på en anpassad VOD-resurs
title: Exempel på en anpassad VOD-resurs
uuid: 21e83b47-d7e2-4a2d-8a0b-80dd09e253a8
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Exempel på en anpassad VOD-resurs {#example-of-a-customized-vod-asset}

Här är ett exempel på en anpassad VOD-resurs:

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:7
 
#EXT-X-ASSET:AID=10
 
#EXTINF:9.9766,
seg1.ts
 
#EXTINF:9.9766,
seg2.ts
 
#EXTINF:9.9766,
seg3.ts
 
#EXT-X-AD:DURATION=10
#EXTINF:9.9766,
seg4.ts
 
#EXTINF:9.9766,
seg5.ts
 
#EXT-X-ENDLIST
```

Programmet kan konfigurera följande scenarier:

* Ett meddelande när det finns `#EXT-X-ASSET` taggar, eller andra uppsättningar anpassade taggnamn som du prenumererar på, i filen.
* Infoga annonser när en `#EXT-X-AD` tagg eller något annat anpassat taggnamn hittas i strömmen.

