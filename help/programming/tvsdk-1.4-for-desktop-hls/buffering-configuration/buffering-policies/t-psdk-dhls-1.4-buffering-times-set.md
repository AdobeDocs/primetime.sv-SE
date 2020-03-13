---
description: MediaPlayer innehåller metoder för att ställa in och hämta den inledande buffringstiden och uppspelningsbuffringstiden.
seo-description: MediaPlayer innehåller metoder för att ställa in och hämta den inledande buffringstiden och uppspelningsbuffringstiden.
seo-title: Ange buffringstider
title: Ange buffringstider
uuid: 25142b01-5381-49c9-b89a-24c858faaf13
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Ange buffringstider{#set-buffering-times}

MediaPlayer innehåller metoder för att ställa in och hämta den inledande buffringstiden och uppspelningsbuffringstiden.

>[!TIP]
>
>Om du inte anger parametrar för buffertkontroll innan uppspelningen startar, blir mediaspelaren som standard 2 sekunder för den inledande bufferten och 30 sekunder för den pågående uppspelningsbufferttiden.

1. Ställ in `BufferControlParameters` objektet, som kapslar in den inledande buffringstiden och tidskontrollparametrarna för uppspelningsbufferten:

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

1. Använd den här `MediaPlayer` metoden om du vill ange värden för buffertparametern:

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. Använd den här `MediaPlayer` metoden om du vill hämta de aktuella buffertparametervärdena:

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Om du till exempel vill ställa in den inledande bufferten på 2 sekunder och uppspelningsbufferttiden på 30 sekunder:

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

I exemplet `psdkdemo` visas denna funktion. Använd programmets inställningar för att ange buffertvärden.
