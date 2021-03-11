---
description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 är ett gemensamt gränssnitt för att spela upp videoannonser. Det ger en multimedieupplevelse för användarna och gör det möjligt för utgivare att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll.
title: Stöd för VPAID 2.0
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# Stöd för VPAID 2.0 och {#vpaid-ad-support}

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
* Annonsering av VPAID efter registrering

## API-ändringar {#section_D62F3E059C6C493592D34534B0BFC150}

Följande ändringar har gjorts i API:t:

* `PTAuditudeMetadata` har en  `customAdLoadTimeout` egenskap som ändrar standardtidsgränsen för VPAID-inläsningsprocessen.

   Standardvärdet för timeout är 10 sekunder.

* `PTMediaPlayerCustomAdNotification` skickas från  `PTMediaPlayer` instansen

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Under uppspelningen av VPAID-annonsen:

* VPAID-annonsen visas i en visningsbehållare ovanför spelarvyn, så koden som är beroende av att användarna trycker på spelarvyn fungerar inte.
* Huvudinnehållsspelaren är pausad och anrop till `pause` och `play` på spelarinstansen används för att pausa och återuppta annonsen för VPAID.

* VPAID-annonser har ingen fördefinierad varaktighet eftersom annonsen kan vara interaktiv.

   Annonsens längd och varaktighet för den totala annonsbrytningen som definieras av annonsserverns svar kanske inte är korrekt.

## Implementera VPAID 2.0-integrering {#section_63C9C737367C4A0AB4D62E0DC2084141}

Så här lägger du till stöd för VPAID 2.0 i ditt iOS-program:

1. (Valfritt) Lägg till en avlyssnare för anpassade annonshändelser.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerCustomAdNotification:) name:PTMediaPlayerCustomAdNotification object:self.player];
   ```

1. (Valfritt) Visa meddelandet.

   ```
   -(void)onMediaPlayerCustomAdNotification:(NSNotification *)notification{    PTCustomAdNotificationObject *notificationObject = [notification.userInfo objectForKey:PTCustomAdNotificationObjectKey];    if (notificationObject)    
   {        NSLog(@"ViewController:: Custom Ad Notification Received: %ld", notificationObject.type);    } 
   
   }
   ```

