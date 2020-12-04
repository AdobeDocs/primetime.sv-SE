---
description: TVSDK buffrar ibland videoströmmen för att ge en jämnare tittarupplevelse. Du kan konfigurera hur spelaren buffrar.
seo-description: TVSDK buffrar ibland videoströmmen för att ge en jämnare tittarupplevelse. Du kan konfigurera hur spelaren buffrar.
seo-title: Buffring
title: Buffring
uuid: 7f9f0deb-5f18-441d-b7a4-67c631a798f4
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---


# Översikt {#buffering-overview}

TVSDK buffrar ibland videoströmmen för att ge en jämnare tittarupplevelse. Du kan konfigurera hur spelaren buffrar.

TVSDK definierar en uppspelningsbuffertlängd på minst 30 sekunder och en inledande bufferttid innan mediet börjar spelas upp på minst 2 sekunder. När programmet har anropat `play`, men innan uppspelningen börjar, buffrar TVSDK mediet till den inledande tiden för att ge en jämn start när uppspelningen faktiskt börjar.

Du kan ändra buffringstiderna genom att definiera nya buffringsprinciper, och du kan ändra när den inledande buffringen inträffar genom att använda Direkt on.

## Bufferttidsprinciper {#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

Beroende på din miljö (inklusive enheten, operativsystemet eller nätverksförhållandena) kan du ange olika buffringsprinciper för spelaren, till exempel ändra minimilängden för inledande buffring och för pågående uppspelningsbuffring.

När du har anropat `play` börjar mediespelaren buffra videon. När mediespelaren har buffrat den mängd video som anges av den inledande buffringstiden börjar uppspelningen. Den här processen förbättrar starttiden eftersom spelaren inte väntar på att hela uppspelningsbufferten ska fyllas innan uppspelningen startas. Efter att de få inledande sekunderna har buffrats börjar uppspelningen i stället.

När videon återges fortsätter TVSDK att buffra nya fragment tills det har buffrat den mängd som anges av uppspelningsbufferttiden. Om den aktuella buffertlängden sjunker under uppspelningsbuffertens tid hämtar spelaren ytterligare fragment. När den aktuella buffertlängden är över uppspelningsbufferttiden med några sekunder kommer TVSDK att sluta hämta fragment.

>[!TIP]
>
>Om det inledande buffertvärdet är högt kan det ge användaren en lång inledande buffringstid innan start. Detta kan ge en jämnare uppspelning under en längre tid. Men om nätverksförhållandena är dåliga kan den inledande uppspelningen fördröjas.

Om du aktiverar direkt genom att anropa `prepareBuffer` börjar den inledande buffringen vid den tidpunkten i stället för att vänta på `play`.

## Ange buffringstider {#section_05CDD927869D47EBA1D2069B1416B2E4}

`MediaPlayer` innehåller metoder för att ställa in och hämta den inledande buffringstiden och uppspelningsbuffringstiden.

>[!TIP]
>
>Om du inte anger parametrar för buffertkontroll innan uppspelningen startar, blir mediaspelaren som standard 2 sekunder för den inledande bufferten och 30 sekunder för den pågående uppspelningsbufferttiden.

1. Ställ in objektet `BufferControlParameters`, som kapslar in den inledande bufferttiden och kontrollparametrarna för uppspelningsbuffertens tid.

   Den här klassen innehåller följande fabriksmetoder:

   * Så här anger du den inledande bufferttiden som motsvarar uppspelningsbufferttiden:

      ```
      public static BufferControlParameters createSimple(long bufferTime)
      ```

   * Så här anger du inledande och uppspelande bufferttider:

      ```
      public static BufferControlParameters createDual( 
        long initialBuffer,  
        long bufferTime)
      ```
   Om parametrarna inte är giltiga, kommer dessa metoder att resultera i `MediaPlayerException` med felkoden `PSDKErrorCode.INVALID_ARGUMENT`, till exempel när följande villkor uppfylls:

   * Den inledande bufferttiden är mindre än noll.
   * Den inledande bufferttiden är längre än bufferttiden.


1. Använd den här `MediaPlayer`-metoden om du vill ange värden för buffertparametrar:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. Använd den här `MediaPlayer`-metoden för att hämta de aktuella buffertparametervärdena:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

Om du till exempel vill ställa in den inledande bufferten på 5 sekunder och uppspelningsbufferttiden på 30 sekunder:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
