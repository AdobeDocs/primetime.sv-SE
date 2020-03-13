---
description: Du kan implementera ett kontrollfält med DVR-stöd för VOD och direktuppspelning. DVR-stödet innefattar begreppet sökbart fönster och klientens direktpunkt.
seo-description: Du kan implementera ett kontrollfält med DVR-stöd för VOD och direktuppspelning. DVR-stödet innefattar begreppet sökbart fönster och klientens direktpunkt.
seo-title: Skapa ett kontrollfält förbättrat för DVR
title: Skapa ett kontrollfält förbättrat för DVR
uuid: c9c86383-379f-452c-b35d-447ac8691fa0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Skapa ett kontrollfält förbättrat för DVR{#construct-a-control-bar-enhanced-for-dvr}

Du kan implementera ett kontrollfält med DVR-stöd för VOD och direktuppspelning. DVR-stödet innefattar begreppet sökbart fönster och klientens direktpunkt.

* För VOD är längden på det sökbara fönstret längden på hela resursen.
* För direktuppspelning definieras längden på DVR-fönstret (sökbart) som det tidsintervall som börjar vid direktuppspelningsfönstret och slutar vid klientens direktpunkt.

   Klientens direktpunkt beräknas genom att den buffrade längden subtraheras från livefönstrets slut. Målets varaktighet är ett värde som är större än eller lika med den maximala längden för ett fragment i manifestet.

   Standardvärdet är 10000 ms.

   Kontrollfältet för direktuppspelning stöder DVR genom att först placera tummen vid klientens direktpunkt när uppspelningen startar och genom att visa ett område som markerar det område där sökning inte är tillåten.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width=&quot;684&quot;}

1. Om du vill implementera ett kontrollfält med DVR-stöd följer du stegen för att visa en sökningslist med några små skillnader:

   * Du kan välja att implementera ett kontrollfält som bara är mappat för det sökbara intervallet i stället för för uppspelningsintervallet. All användarinteraktion för sökning kan anses vara säker i sökbart intervall.
   * Du kan välja att implementera ett kontrollfält som är mappat för uppspelningsintervallet, men som även visar det sökbara intervallet.

      För ett kontrollfält:
   1. Lägg till en övertäckning i kontrollfältet som representerar uppspelningsintervallet.
   1. När användaren börjar söka kontrollerar du om den önskade sökpositionen ligger inom det sökbara intervallet med `MediaPlayer.getSeekableRange`.

      Exempel:

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      Du kan också välja att söka till klientens direktpunkt med hjälp av `MediaPlayer.LIVE_POINT` -konstanten.

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```
