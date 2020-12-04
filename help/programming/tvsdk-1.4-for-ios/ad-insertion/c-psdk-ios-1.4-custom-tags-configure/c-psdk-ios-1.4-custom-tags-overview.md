---
seo-title: Exempel på en anpassad VOD-resurs
title: Exempel på en anpassad VOD-resurs
uuid: e0dfaa72-d62f-4fb3-b7c5-ad94f0dc7ce0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
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

* Det finns ett meddelande när `#EXT-X-ASSET`-taggar eller andra uppsättningar anpassade taggnamn som du har prenumererat på finns i filen.
* Infoga annonser när en `#EXT-X-AD`-tagg eller något annat anpassat taggnamn hittas i strömmen.

