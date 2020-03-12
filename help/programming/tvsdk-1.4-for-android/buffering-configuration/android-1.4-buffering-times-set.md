---
description: TVSDK buffrar ibland videoströmmen för att ge en jämnare tittarupplevelse. Du kan konfigurera hur spelaren buffrar.
seo-description: TVSDK buffrar ibland videoströmmen för att ge en jämnare tittarupplevelse. Du kan konfigurera hur spelaren buffrar.
seo-title: Ange buffringstider
title: Ange buffringstider
uuid: 5a3945a4-1935-4797-b19d-84989850a487
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Buffring {#buffering}

TVSDK buffrar ibland videoströmmen för att ge en jämnare tittarupplevelse. Du kan konfigurera hur spelaren buffrar.

TVSDK definierar en uppspelningsbuffertlängd på minst 30 sekunder och en inledande bufferttid inom denna, innan mediet börjar spelas upp, på minst 2 sekunder. När programmet har anropat `play` men innan uppspelningen börjar buffrar TVSDK mediet till den inledande tiden för att ge en jämn start när uppspelningen faktiskt börjar.

Du kan ändra buffringstiderna genom att definiera nya buffringsprinciper och du kan ändra när den inledande buffringen inträffar med hjälp av direktaktivering.

## Ange buffringstider {#set-buffering-times}

I `MediaPlayer` finns metoder för att ställa in och hämta den inledande buffringstiden och uppspelningsbuffringstiden.

>[!TIP]
>
>Om du inte anger parametrar för buffertkontroll innan uppspelningen startar, blir mediaspelaren som standard 2 sekunder för den inledande bufferten och 30 sekunder för den pågående uppspelningsbufferttiden.

1. Ställ in `BufferControlParameters` objektet, som kapslar in den inledande buffringstiden och tidskontrollparametrarna för uppspelningsbufferten:

       Den här klassen innehåller två fabriksmetoder:
   
   * Så här anger du den inledande bufferttiden som motsvarar uppspelningsbufferttiden:

      ```java
      public static BufferControlParameters createSimple( 
          long bufferTime)
      ```

   * Så här anger du både inledande och uppspelad bufferttid:

      ```java
      public static BufferControlParameters createDual( 
          long initialBuffer,   
          long bufferTime)
      ```

      Dessa metoder genererar ett `IllegalArgumentException` om parametrarna inte är giltiga, till exempel när:

   * Den inledande bufferttiden är mindre än noll.
   * Den inledande bufferttiden är längre än bufferttiden.

1. Använd den här `MediaPlayer` metoden om du vill ange värden för buffertparametern:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. Använd den här `MediaPlayer` metoden om du vill hämta de aktuella buffertparametervärdena:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

   Om AVE inte kan ange de angivna värdena försätts mediespelaren i `ERROR` läge med felkoden `SET_BUFFER_PARAMETERS_ERROR`.

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Om du till exempel vill ställa in den inledande bufferten på 2 sekunder och uppspelningsbufferttiden på 30 sekunder:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

Primetimes referensimplementering demonstrerar denna funktion; Använd programmets inställningar för att ange buffertvärden.