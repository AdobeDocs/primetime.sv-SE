---
description: Programmet måste använda rätt TimedMetadata-objekt vid rätt tidpunkt.
title: Lagra tidsbestämda metadataobjekt när de skickas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Lagra tidsbestämda metadataobjekt när de skickas {#store-timed-metadata-objects-as-they-are-dispatched}

Programmet måste använda rätt TimedMetadata-objekt vid rätt tidpunkt.

Under innehållsparsning, som inträffar före uppspelning, identifierar TVSDK prenumerationstaggar och meddelar programmet om dessa taggar. Tiden som associeras med varje `TimedMetadata` är lokal tid på uppspelningstidslinjen.

Programmet måste utföra följande uppgifter:

1. Håll reda på aktuell uppspelningstid.
1. Matcha aktuell uppspelningstid med skickade `TimedMetadata`-objekt.

1. Använd `TimedMetadata` där starttiden är lika med den aktuella lokala uppspelningstiden.

   I följande exempel visas hur du sparar `TimedMetadata`-objekt i en `ArrayList`.

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

