---
description: Du kan ange format, till exempel teckensnitt, storlek, färg, kant och opacitet för undertextad text.
seo-description: Du kan ange format, till exempel teckensnitt, storlek, färg, kant och opacitet för undertextad text.
seo-title: Ange format för undertexter
title: Ange format för undertexter
uuid: 906ed22c-e673-4211-a14b-d95d176aad21
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Ange format för undertexter{#set-closed-caption-styles}

Du kan ange format, till exempel teckensnitt, storlek, färg, kant och opacitet för undertextad text.

1. Vänta tills `MediaPlayer` den är åtminstone i tillståndet PREPARED.

   Mer information om lägena finns i [Vänta på ett giltigt tillstånd](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md).
1. Skapa en `TextFormat` instans.

   Du kan ange alla parametrar för textningsformat nu eller ange dem senare.

   ```js
   new TextFormat( 
       font,   
       fontColor,  
       edgeColor,   
       fontEdge,  
       backgroundColor,   
       fillColor,  
       size,   
       fontOpacity,   
       backgroundOpacity,  
       fillOpacity, 
       bottomInset 
       safeArea) → {AdobePSDK.TextFormat}
   ```

1. (Valfritt) Hämta de aktuella stilinställningarna för undertextning med `MediaPlayer.ccStyle`.

   Returvärdet är en instans av `TextFormat` gränssnittet.

   Om inget format har angetts tidigare returneras ett TextFormat-objekt med standardvärden för varje attribut:

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. Om du vill ändra formatinställningarna använder du `MediaPlayer.ccStyle`och skickar en instans av `TextFormat` gränssnittet.

   Du kan använda den här metoden även om den aktuella medieströmmen inte har några undertexter.

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >Det kan ta några sekunder innan ändringarna visas på skärmen att ställa in stilen för undertextning asynkront.

