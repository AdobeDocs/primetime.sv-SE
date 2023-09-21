---
description: Programmet måste använda rätt TimedMetadata-objekt vid rätt tidpunkt.
title: Lagra tidsbestämda metadataobjekt när de skickas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Lagra tidsbestämda metadataobjekt när de skickas {#store-timed-metadata-objects-as-they-are-dispatched}

Programmet måste använda rätt TimedMetadata-objekt vid rätt tidpunkt.

Under innehållsparsning, som inträffar före uppspelning, identifierar TVSDK prenumerationstaggar och meddelar programmet om dessa taggar. Den tid som associeras med varje `TimedMetadata` är lokal tid på uppspelningstidslinjen.

Programmet måste utföra följande uppgifter:

1. Håll reda på aktuell uppspelningstid.
1. Matcha den aktuella uppspelningstiden med den skickade `TimedMetadata` objekt.

1. Använd `TimedMetadata` där starttiden motsvarar den aktuella lokala uppspelningstiden.

   I följande exempel visas hur du sparar `TimedMetadata` objekt i en `ArrayList`.

   ```java
   private List<TimedMetadata> _timedMetadataList = new ArrayList<TimedMetadata>(); 
   ... 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       ... 
       if (timedMetadata.getName().equalsIgnoreCase("#EXT-X-CUE"))  { 
           _timedMetadataList.add(timedMetadata); 
       } 
       ... 
   }
   ```
