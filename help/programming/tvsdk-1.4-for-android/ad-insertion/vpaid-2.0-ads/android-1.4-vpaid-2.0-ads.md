---
description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 är ett gemensamt gränssnitt för att spela upp videoannonser. Det ger en multimedieupplevelse för användarna och gör det möjligt för utgivare att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll.
seo-description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 är ett gemensamt gränssnitt för att spela upp videoannonser. Det ger en multimedieupplevelse för användarna och gör det möjligt för utgivare att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll.
seo-title: Stöd för VPAID 2.0
title: Stöd för VPAID 2.0
uuid: 7168a6e4-9c5e-4d3a-8710-867cf98e4445
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Stöd för VPAID 2.0 {#vpaid-ad-support}

Video Player Ad-Serving Interface Definition (VPAID) 2.0 är ett gemensamt gränssnitt för att spela upp videoannonser. Det ger en multimedieupplevelse för användarna och gör det möjligt för utgivare att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll.

Följande funktioner stöds:

* Version 2.0 av VPAID-specifikationen

   Mer information finns i [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Linjära VPAID-annonser om VOD-innehåll (video-on-demand)
* JavaScript VPAID-annonser

   VPAID-annonser måste vara JavaScript-baserade, och annonssvaret måste identifiera medietypen för VPAID-annonsen som `application/javascript`.

Följande funktioner stöds inte:

* Version 1.0 av VPAID-specifikationen
* Överhoppade annonser
* Annonser som t.ex. övertäckningar, dynamiska följesedlar, minimeringsbara annonser, annonser som kan radbytas och expanderbara annonser
* Förhandsladda VPAID-annonser
* VPAID-annonser i direktinnehåll
* Flash VPAID-annonser

## API-ändringar {#section_D62F3E059C6C493592D34534B0BFC150}

Följande ändringar har gjorts i API:t:

* En `getCustomAdView` funktion har lagts till i `MediaPlayer` och returnerar webbvyn som återger VPAID-annonsen.

   Mer information om det objekt `CustomAdView` som returneras av den här funktionen finns i [API-referenser](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/index.html).

* En `CUSTOM_AD` händelse skickas från mediespelarinstansen.

   Programmet kan registrera ett händelseåteranrop genom att implementera `CustomAdEventListener`.

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` gör att du kan ändra standardtimeout för VPAID-inläsningsprocessen.

   Standardvärdet för timeout är 10 sekunder.

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Under uppspelningen av VPAID-annonsen:

* VPAID-annonsen visas i en visningsbehållare ovanför spelarvyn, så koden som är beroende av att användarna trycker på spelarvyn fungerar inte.
* Huvudinnehållsspelaren pausas och anrop till `pause` och `play` på spelarinstansen används för att pausa och återuppta VPAID-annonsen.

* VPAID-annonser har ingen fördefinierad varaktighet eftersom annonsen kan vara interaktiv.

   Annonsens längd och varaktighet för den totala annonsbrytningen som definieras av annonsserverns svar kanske inte är korrekt.

## Implementera VPAID 2.0-integrering {#implement-vpaid-integration}

Om du vill lägga till stöd för VPAID 2.0 lägger du till en anpassad annonsvy och lämpliga avlyssnare.

Så här lägger du till stöd för VPAID 2.0:

1. Lägg till den anpassade annonsvyn i spelargränssnittet.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Lägg till en avlyssnare för anpassade annonshändelser.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```
