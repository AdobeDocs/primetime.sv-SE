---
title: Exempel på en anpassad VOD-resurs
description: Exempel på en anpassad VOD-resurs
copied-description: true
exl-id: 1619d1e8-e315-4109-b0b9-0f1426a8e9f9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# Exempel på en anpassad VOD-resurs{#example-of-a-customized-vod-asset}

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

* Ett meddelande när `#EXT-X-ASSET` -taggar, eller andra uppsättningar egna taggnamn som du har prenumererat på, finns i filen.
* Infoga annonser när en `#EXT-X-AD` -taggen, eller något annat anpassat taggnamn, finns i strömmen.
