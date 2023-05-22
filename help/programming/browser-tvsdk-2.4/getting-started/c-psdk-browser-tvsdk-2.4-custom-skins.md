---
description: Om du vill använda de anpassade skalen måste du skriva en anpassning som liknar default-video-controls.css och hänvisa till den nya anpassningen i spelaren.
title: Anpassade skal
exl-id: 4d627545-942d-4883-a010-afddcffb8dd5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Anpassade skal{#custom-skins}

Om du vill använda de anpassade skalen måste du skriva en anpassning som liknar default-video-controls.css och hänvisa till den nya anpassningen i spelaren.

Du kan till exempel använda något av följande alternativ:

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

Du kan göra följande typer av ändringar:

* Förgrundsfärg för knappar och text

   Alla kontroller som har en förgrund använder `vid-skin-fgcolor` klassen. Om du vill ändra förgrunden för alla kontroller itererar du igenom alla element med `vid-skin-fgcolor` och ange önskad färg.
* Bakgrundsfärg för knappar och text

   Alla kontroller som har en förgrund använder `vid-skin-bgcolor` klassen. Om du vill ändra förgrunden för alla kontroller itererar du igenom alla element med `vid-skin-bgcolor` och ange önskad färg.
* Spelhuvudets form

   Spelhuvudet kan vara fyrkantigt eller runt. Om du vill ändra spelhuvudet lägger du till `square` eller `round` klass till `playhead` -element.
* Buffertspinnarnas format

   Referensspelaren innehåller följande stilar för att dela upp när spelaren buffrar innehåll:

   * Överläggningstext ( `overlay-text`)
   * Rektangulär snurra ( `spinner`)
   * Signal ( `signal`)
   * Lodräta streck ( `vertical`)

      >[!TIP]
      >
      >Om du vill använda någon av buffertspinnarna måste du lägga till klassen i elementet buffering-overlay. Använd till exempel `overlay-text`lägger du till följande rader i `BufferOverlay.js` fil:
      >
      >
      ```js
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```
