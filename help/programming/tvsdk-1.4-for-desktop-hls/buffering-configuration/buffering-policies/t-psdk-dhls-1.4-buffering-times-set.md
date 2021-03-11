---
description: MediaPlayer innehåller metoder för att ställa in och hämta den inledande buffringstiden och uppspelningsbuffringstiden.
title: Ange buffringstider
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Ange buffringstider{#set-buffering-times}

MediaPlayer innehåller metoder för att ställa in och hämta den inledande buffringstiden och uppspelningsbuffringstiden.

>[!TIP]
>
>Om du inte anger parametrar för buffertkontroll innan uppspelningen startar, blir mediaspelaren som standard 2 sekunder för den inledande bufferten och 30 sekunder för den pågående uppspelningsbufferttiden.

1. Ställ in objektet `BufferControlParameters`, som kapslar in den inledande bufferttiden och kontrollparametrarna för uppspelningsbuffertens tid:

       Den här klassen innehåller följande fabriksmetoder:
   
   * Så här anger du den inledande bufferttiden som motsvarar uppspelningsbufferttiden:

      ```
      createSimple(bufferTime:uint):BufferControlParameters
      ```

   * Så här anger du både inledande och uppspelad bufferttid:

      ```
      createDual(initialBufferTime:uint, playbackBufferTime:uint):BufferControlParameters 
      ```

      Dessa metoder genererar ett `IllegalArgumentException` om parametrarna inte är giltiga, till exempel när:

   * Den inledande bufferttiden är mindre än noll.
   * Den inledande bufferttiden är längre än bufferttiden.

1. Använd den här `MediaPlayer`-metoden om du vill ange värden för buffertparametern:

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. Använd den här `MediaPlayer`-metoden för att hämta de aktuella buffertparametervärdena:

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Om du till exempel vill ställa in den inledande bufferten på 2 sekunder och uppspelningsbufferttiden på 30 sekunder:

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

`psdkdemo` demonstrerar den här funktionen; Använd programmets inställningar för att ange buffertvärden.
