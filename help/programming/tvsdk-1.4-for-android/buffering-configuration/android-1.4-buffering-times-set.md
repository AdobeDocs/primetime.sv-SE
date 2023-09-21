---
description: TVSDK buffrar ibland videoströmmen för att ge en jämnare tittarupplevelse. Du kan konfigurera hur spelaren buffrar.
title: Ange buffringstider
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Buffring {#buffering}

TVSDK buffrar ibland videoströmmen för att ge en jämnare tittarupplevelse. Du kan konfigurera hur spelaren buffrar.

TVSDK definierar en uppspelningsbuffertlängd på minst 30 sekunder och en inledande bufferttid inom denna, innan mediet börjar spelas upp, på minst 2 sekunder. Efter programanrop `play` men innan uppspelningen börjar buffrar TVSDK mediet tills det börjar spelas upp, vilket ger en mjuk start när uppspelningen börjar.

Du kan ändra buffringstiderna genom att definiera nya buffringsprinciper och du kan ändra när den inledande buffringen inträffar med hjälp av direktaktivering.

## Ange buffringstider {#set-buffering-times}

The `MediaPlayer` innehåller metoder för att ställa in och hämta den inledande buffringstiden och uppspelningsbuffringstiden.

>[!TIP]
>
>Om du inte anger parametrar för buffertkontroll innan uppspelningen startar, blir mediaspelaren som standard 2 sekunder för den inledande bufferten och 30 sekunder för den pågående uppspelningsbufferttiden.

1. Konfigurera `BufferControlParameters` object, som kapslar in den inledande bufferttiden och kontrollparametrarna för uppspelningsbuffertens tid:

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

     Dessa metoder genererar `IllegalArgumentException` om parametrarna inte är giltiga, till exempel när:

   * Den inledande bufferttiden är mindre än noll.
   * Den inledande bufferttiden är längre än bufferttiden.

1. Om du vill ange värden för buffertparametrar använder du följande `MediaPlayer` metod:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. Använd det här alternativet om du vill hämta de aktuella buffertparametervärdena `MediaPlayer` metod:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

   Om AVE inte kan ange de angivna värdena, kommer mediespelaren att `ERROR` status med felkoden `SET_BUFFER_PARAMETERS_ERROR`.

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Om du till exempel vill ställa in den inledande bufferten på 2 sekunder och uppspelningsbufferttiden på 30 sekunder:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

Referensimplementeringen för Primetime demonstrerar den här funktionen. Använd programmets inställningar för att ange buffertvärden.
