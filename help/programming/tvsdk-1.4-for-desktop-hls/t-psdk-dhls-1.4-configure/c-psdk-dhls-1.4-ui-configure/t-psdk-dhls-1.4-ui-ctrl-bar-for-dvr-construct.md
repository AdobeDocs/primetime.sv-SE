---
description: Du kan implementera ett kontrollfält med DVR-stöd för VOD och direktuppspelning. DVR-stödet innefattar begreppet sökbart fönster och klientens direktpunkt.
title: Skapa ett kontrollfält förbättrat för DVR
exl-id: 8e70f03c-880a-48c5-8728-a4b967c19925
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Skapa ett kontrollfält förbättrat för DVR{#construct-a-control-bar-enhanced-for-dvr}

Du kan implementera ett kontrollfält med DVR-stöd för VOD och direktuppspelning. DVR-stödet innefattar begreppet sökbart fönster och klientens direktpunkt.

* För VOD är längden på det sökbara fönstret längden på hela resursen.
* För direktuppspelning definieras längden på DVR-fönstret (sökbart) som det tidsintervall som börjar vid direktuppspelningsfönstret och slutar vid klientens direktpunkt.

   Klientens direktpunkt beräknas genom att den buffrade längden subtraheras från livefönstrets slut. Målets varaktighet är ett värde som är större än eller lika med den maximala längden för ett fragment i manifestet.

   Standardvärdet är 10000 ms.

   Kontrollfältet för direktuppspelning stöder DVR genom att först placera tummen vid klientens direktpunkt när uppspelningen startar och genom att visa ett område som markerar det område där sökning inte är tillåten.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width="684"}

1. Om du vill implementera ett kontrollfält med DVR-stöd följer du stegen för att visa en sökningslist med några små skillnader:

   * Du kan välja att implementera ett kontrollfält som bara är mappat för det sökbara intervallet i stället för för uppspelningsintervallet. All användarinteraktion för sökning kan anses vara säker i sökbart intervall.
   * Du kan välja att implementera ett kontrollfält som är mappat för uppspelningsintervallet, men som även visar det sökbara intervallet.

      För ett kontrollfält:
   1. Lägg till en övertäckning i kontrollfältet som representerar uppspelningsintervallet.
   1. När användaren börjar söka kontrollerar du om den önskade sökpositionen ligger inom det sökbara intervallet med hjälp av `MediaPlayer.seekableRange` -egenskap.

      Exempel:

      ```
      var desiredPosition:Number = // TODO : choose a value 
      
      private function onStatusChange(event:MediaPlayerStatusChangeEvent):void { 
          switch(event.status) { 
              case MediaPlayerStatus.PREPARED: 
                  _mediaPlayer.prepareToPlay(desiredPosition); 
          } 
      }
      ```

      Du kan också välja att söka till klientens direktpunkt med `MediaPlayer.LIVE_POINT` konstant.

      ```
      private function onSeekToLiveClick(event:MouseEvent):void { 
          _player.seek(DefaultMediaPlayer.LIVE_POINT); 
      }
      ```
