---
description: Programmet måste använda rätt TimedMetadata-objekt vid rätt tidpunkt.
seo-description: Programmet måste använda rätt TimedMetadata-objekt vid rätt tidpunkt.
seo-title: Lagra tidsbestämda metadataobjekt när de skickas
title: Lagra tidsbestämda metadataobjekt när de skickas
uuid: 3d0ed022-829d-474e-83a9-152caeb5b317
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Lagra tidsbestämda metadataobjekt när de skickas {#store-timed-metadata-objects-as-they-are-dispatched}

Programmet måste använda rätt TimedMetadata-objekt vid rätt tidpunkt.

Under innehållsparsning, som inträffar före uppspelning, identifierar TVSDK prenumerationstaggar och meddelar programmet om dessa taggar.

>[!TIP]
>
>Tiden som associeras med varje `TimedMetadata` är lokal tid på uppspelningstidslinjen.

Så här lagrar du tidsbestämda metadataobjekt när de skickas:

1. Håll reda på aktuell uppspelningstid.
1. Matcha aktuell uppspelningstid med skickade `TimedMetadata` objekt.

1. Använd den `TimedMetadata` plats där starttiden är lika med den aktuella lokala uppspelningstiden.

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

