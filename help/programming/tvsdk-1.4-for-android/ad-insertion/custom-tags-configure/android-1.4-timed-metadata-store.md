---
description: Programmet måste använda rätt TimedMetadata-objekt vid rätt tidpunkt.
seo-description: Programmet måste använda rätt TimedMetadata-objekt vid rätt tidpunkt.
seo-title: Lagra tidsbestämda metadataobjekt när de skickas
title: Lagra tidsbestämda metadataobjekt när de skickas
uuid: 0e6d2a42-37a8-477e-b925-66bbc23445c1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '138'
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

