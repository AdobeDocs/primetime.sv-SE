---
description: Om du vill använda de anpassade skalen måste du skriva en anpassning som liknar default-video-controls.css och hänvisa till den nya anpassningen i spelaren.
seo-description: Om du vill använda de anpassade skalen måste du skriva en anpassning som liknar default-video-controls.css och hänvisa till den nya anpassningen i spelaren.
seo-title: Anpassade skal
title: Anpassade skal
uuid: bc71926e-0dec-4628-8248-911224a7a6c2
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Anpassade skal{#custom-skins}

Om du vill använda de anpassade skalen måste du skriva en anpassning som liknar default-video-controls.css och hänvisa till den nya anpassningen i spelaren.

Du kan till exempel använda något av följande alternativ:

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

Du kan göra följande typer av ändringar:

* Förgrundsfärg för knappar och text

   Alla kontroller som har en förgrund använder klassen `vid-skin-fgcolor`. Om du vill ändra förgrunden för alla kontroller itererar du igenom alla element med klassen `vid-skin-fgcolor` och anger önskad färg.
* Bakgrundsfärg för knappar och text

   Alla kontroller som har en förgrund använder klassen `vid-skin-bgcolor`. Om du vill ändra förgrunden för alla kontroller itererar du igenom alla element med klassen `vid-skin-bgcolor` och anger önskad färg.
* Spelhuvudets form

   Spelhuvudet kan vara fyrkantigt eller runt. Om du vill ändra spelhuvudet lägger du till `square` eller `round`-klassen i `playhead`-elementet.
* Buffertspinnarnas format

   Referensspelaren innehåller följande stilar för att dela upp när spelaren buffrar innehåll:

   * Överläggningstext ( `overlay-text`)
   * Rektangulär snurra ( `spinner`)
   * Signal ( `signal`)
   * Lodräta staplar ( `vertical`)

      >[!TIP]
      >
      >Om du vill använda någon av buffertspinnarna måste du lägga till klassen i elementet buffering-overlay. Om du till exempel vill använda `overlay-text` lägger du till följande rader i `BufferOverlay.js`-filen:
      >
      >
      ```js
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```

