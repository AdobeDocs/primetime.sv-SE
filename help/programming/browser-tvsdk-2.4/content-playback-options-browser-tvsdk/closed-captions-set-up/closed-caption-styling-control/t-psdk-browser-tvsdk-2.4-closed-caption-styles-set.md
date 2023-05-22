---
description: Du kan ange format, till exempel teckensnitt, storlek, färg, kant och opacitet för undertextad text.
title: Ange format för undertexter
exl-id: 7ece68ce-0dc5-4899-9834-39940bbd0332
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Ange format för undertexter{#set-closed-caption-styles}

Du kan ange format, till exempel teckensnitt, storlek, färg, kant och opacitet för undertextad text.

1. Vänta på `MediaPlayer` vara åtminstone i FÖRBEREDD form.

   Mer information om lägena finns i [Vänta på ett giltigt tillstånd](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md).
1. Skapa en `TextFormat` -instans.

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

   Returvärdet är en instans av `TextFormat` gränssnitt.

   Om inget format har angetts tidigare returneras ett TextFormat-objekt med standardvärden för varje attribut:

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. Om du vill ändra formatinställningarna använder du `MediaPlayer.ccStyle`, skicka en instans av `TextFormat` gränssnitt.

   Du kan använda den här metoden även om den aktuella medieströmmen inte har några undertexter.

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >Det kan ta några sekunder innan ändringarna visas på skärmen att ställa in stilen för undertextning asynkront.
