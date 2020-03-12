---
description: TVSDK stöder visning av VPAID-annonser (linear Video Player-Ad Interface Definition) i en annonsbrytning. VPAID version 1.0 kräver Flash, medan version 2.0 också fungerar med Browser TVSDK och JavaScript.
seo-description: TVSDK stöder visning av VPAID-annonser (linear Video Player-Ad Interface Definition) i en annonsbrytning. VPAID version 1.0 kräver Flash, medan version 2.0 också fungerar med Browser TVSDK och JavaScript.
seo-title: Visa linjära VPAID-annonser i en annonsbrytning
title: Visa linjära VPAID-annonser i en annonsbrytning
uuid: 1f3a5426-79f5-49a1-a913-923708c09ade
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Visa linjära VPAID-annonser i en annonsbrytning{#display-linear-vpaid-ads-in-an-ad-break}

TVSDK stöder visning av VPAID-annonser (linear Video Player-Ad Interface Definition) i en annonsbrytning. VPAID version 1.0 kräver Flash, medan version 2.0 också fungerar med Browser TVSDK och JavaScript.

Om du vill visa VPAID-annonser korrekt måste du ange en annonsbehållare ( `AdContainerView`) i `MediaPlayerContext` instansen.

Begränsningar för VPAID-annonser:

* VPAID-annonser har inte nödvändigtvis en fördefinierad längd eftersom annonsen kan vara interaktiv. Annonslängden (som definieras av annonsserverns svar) kanske inte alltid motsvarar annonsens verkliga varaktighet.
* För VPAID 1.0-annonser kräver TVSDK att Flash Player 14.0.0.160 eller senare är installerat på enheten. I tidigare versioner av Flash Player är den här funktionen inaktiverad och VPAID 1.0-annonser hoppas över.

Så här ställer du in en annonsbehållare för visning av VPAID-annonser (version 1.0 eller 2.0) inom en annonsbrytning:

1. Använd följande exempelkod för att konfigurera en annonsbehållare som kan visa VPAID-annonser.

   ```
   var context:MediaPlayerContext =  
     new MediaPlayerContext(_authorizedFeatureHelper.authorizedFeatures); 
   
   adContainer = new AdContainerView(); 
   adContainer.x = adContainer.y = 0; 
   adContainer.setSize(videoContainer.width, videoContainer.height); 
   addChild(adContainer); 
   
   context.adContainer = adContainer; 
   _player = new DefaultMediaPlayer(context);
   ```

1. När vyn ändrar storlek återställer du storleken på annonsbehållaren.

   ```
   adContainer.setSize(stage.stageWidth, stage.stageHeight);
   ```

   >[!NOTE]
   >
   >När du får en händelse som ändrar helskärmsläge och anger den nya storleken för annonsbehållaren skickar du scenens visningsläge enligt följande för att säkerställa att spelaren ändrar storlek korrekt:    >
   >
   >
   ```>
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```   >
   >



