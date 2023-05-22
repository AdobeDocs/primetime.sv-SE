---
description: Programmet måste använda rätt TimedMetadata-objekt vid rätt tidpunkt.
title: Lagra tidsbestämda metadataobjekt när de skickas
exl-id: da7ee636-f3ac-4aac-9ca0-7075b8c910f0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Lagra tidsbestämda metadataobjekt när de skickas {#store-timed-metadata-objects-as-they-are-dispatched}

Programmet måste använda rätt TimedMetadata-objekt vid rätt tidpunkt.

Under innehållsparsning, som inträffar före uppspelning, identifierar TVSDK prenumerationstaggar och meddelar programmet om dessa taggar.

>[!TIP]
>
>Den tid som associeras med varje `TimedMetadata` är lokal tid på uppspelningstidslinjen.

Så här lagrar du tidsbestämda metadataobjekt när de skickas:

1. Håll reda på aktuell uppspelningstid.
1. Matcha den aktuella uppspelningstiden med den skickade `TimedMetadata` objekt.

1. Använd `TimedMetadata` där starttiden är lika med den aktuella lokala uppspelningstiden.

   I följande exempel visas hur du sparar `TimedMetadata` objekt i en `ArrayList`.

   ```java
   private List<TimedMetadata> _timedMetadataList =  
     new ArrayList<TimedMetadata>(); 
   ... 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       ... 
       if (timedMetadata.getName().equalsIgnoreCase("#EXT-X-CUE"))  { 
           _timedMetadataList.add(timedMetadata); 
       } 
       ... 
   }
   ```
