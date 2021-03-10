---
description: Du kan ange formatinformation för textningsspår med klassen TextFormat. Detta anger formatet för alla undertexter som visas av spelaren.
title: Styr textningsformat
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---


# Kontroll av textningsformat {#control-closed-caption-styling-overview}

Du kan ange formatinformation för textningsspår med klassen TextFormat. Detta anger formatet för alla undertexter som visas av spelaren.

Den här klassen kapslar in formatinformation för undertexter som teckensnittstyp, storlek, färg och bakgrundsopacitet. En associerad hjälpklass, `TextFormatBuilder`, underlättar arbetet med formatinställningar för undertexter.

## Ange format för undertexter {#set-closed-caption-styles}

Du kan formatera undertexttexten med TVSDK-metoder.

1. Vänta tills mediespelaren är i åtminstone tillståndet PREPARED.
1. Skapa en `TextFormatBuilder`-instans.

   Du kan ange alla parametrar för textningsformat nu eller ange dem senare.

   TVSDK kapslar in formatinformation för undertexter i `TextFormat`-gränssnittet. Klassen `TextFormatBuilder` skapar objekt som implementerar det här gränssnittet.

   ```java
   public TextFormatBuilder( 
      Font font, 
      Size size, 
      FontEdge fontEdge, 
      Color fontColor, 
      Color backgroundColor, 
      Color fillColor, 
      Color edgeColor, 
      int fontOpacity, 
      int backgroundOpacity, 
      int fillOpacity)
   ```

1. Om du vill få en referens till ett objekt som implementerar gränssnittet `TextFormat` anropar du den publika metoden `TextFormatBuilder.toTextFormat`.

   Detta returnerar ett `TextFormat`-objekt som kan tillämpas på mediespelaren.

   ```java
   public TextFormat toTextFormat()
   ```

1. Du kan även hämta de aktuella stilinställningarna för undertextning genom att göra något av följande:

   * Hämta alla formatinställningar med `MediaPlayer.getCCStyle`.

      Returvärdet är en instans av `TextFormat`-gränssnittet.

      ```js
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws IllegalStateException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws IllegalStateException;
      ```

   * Hämta inställningarna en åt gången med hjälp av metoderna för att hämta i gränssnittet i `TextFormat`.

      ```js
      public Color getFontColor(); 
      public Color getBackgroundColor(); 
      public Color getFillColor(); // retrieve the font fill color 
      public Color getEdgeColor(); // retrieve the font edge color 
      public Size getSize(); // retrieve the font size 
      public FontEdge getFontEdge(); // retrieve the font edge type 
      public Font getFont(); // retrieve the font type 
      public int getFontOpacity(); 
      public int getBackgroundOpacity();
      ```

1. Gör något av följande om du vill ändra formatinställningarna:

   >[!NOTE]
   >
   >Du kan inte ändra storleken för WebVTT-bildtexter.

   * Använd metoden `MediaPlayer.setCCStyle` och skicka en instans av gränssnittet `TextFormat`:

      ```js
      /** 
      * Sets the closed captioning style. Used to control the closed captioning font, 
      * size, color, edge and opacity.  
      * 
      * This method is safe to use even if the current media stream doesn't have closed 
      * captions. 
      * 
      * @param textFormat 
      * @throws IllegalStateException 
      */ 
      public void setCCStyle(TextFormat textFormat) throws IllegalStateException;
      ```

   * Använd klassen `TextFormatBuilder` som definierar enskilda set-metoder.

      Gränssnittet `TextFormat` definierar ett objekt som inte kan ändras, så det finns bara get-metoder och inga set-metoder. Du kan bara ange parametrar för textningsformat med klassen `TextFormatBuilder`:

      ```js
      // set font type 
      public void setFont(Font font)  
      public void setBackgroundColor(Color backgroundColor) 
      public void setFillColor(Color fillColor) 
      // set the font-edge color 
      public void setEdgeColor(Color edgeColor)  
      // set the font size 
      public void setSize(Size size)  
      // set the font edge type 
      public void setFontEdge(FontEdge fontEdge)  
      public void setFontOpacity(int fontOpacity) 
      public void setBackgroundOpacity(int backgroundOpacity) 
      // set the font-fill opacity level 
      public void setFillOpacity(int fillOpacity)  
      public void setFontColor(Color fontColor)
      ```

Att ställa in stilen för undertexter är en asynkron åtgärd, så det kan ta upp till några sekunder innan ändringarna visas på skärmen.

## Alternativ för textningsformat {#closed-caption-styling-options}

Du kan ange flera alternativ för bildtextformat och de här alternativen åsidosätter formatalternativen i de ursprungliga bildtexterna

```
public TextFormatBuilder(
 Font font,
 Size size,
 FontEdge fontEdge,
 Color fontColor,
 Color backgroundColor,
 Color fillColor,
 Color edgeColor,
 int fontOpacity,
 int backgroundOpacity,
 int fillOpacity,
 String bottomInset)
```

>[!TIP]
>
>I alternativ som definierar standardvärden (till exempel DEFAULT) refererar det värdet till inställningen som var när bildtexten ursprungligen angavs.

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b> Format </b></th> 
   <th colname="2" class="entry"> <b>Beskrivning</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> Teckensnitt </td> 
   <td colname="2"> <p>Teckensnittstypen. </p> <p>Kan endast anges till ett värde som definieras av uppräkningen <span class="codeph"> TextFormat.Font </span> och representerar till exempel fast teckenbredd med eller utan serifer. </p> <p>Tips:  De faktiska teckensnitten som finns på en enhet kan variera, och ersättningar används vid behov. Monospace med serifer används vanligtvis som ersättning, men den här ersättningen kan vara systemspecifik. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Storlek </td> 
   <td colname="2"> <p>Bildtextens storlek. </p> <p> Kan endast anges till ett värde som definieras av uppräkningen <span class="codeph"> TextFormat.Size </span>: 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MEDIUM  </span> - Standardstorlek </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> STOR  </span> - Cirka 30 % större än mediet </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> SMALL  </span> - Cirka 30 % mindre än medel </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> STANDARD  </span> - Bildtextens standardstorlek; samma som medium </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Teckensnittskant </td> 
   <td colname="2"> <p>Den effekt som används för teckensnittskanten, till exempel upphöjd eller ingen. </p> <p>Kan endast anges till ett värde som definieras av uppräkningen <span class="codeph"> TextFormat.FontEdge </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Teckenfärg </td> 
   <td colname="2"> <p>Teckenfärgen. </p> <p>Kan endast anges till ett värde som definieras av uppräkningen <span class="codeph"> TextFormat.Color </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Kantfärg </td> 
   <td colname="2"> <p>Färgen på kanteffekten. </p> <p>Kan ställas in på något av de värden som är tillgängliga för teckensnittsfärgen. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Bakgrundsfärg </td> 
   <td colname="2"> <p>Bakgrundsteckencellens färg. </p> <p>Kan endast anges med värden som är tillgängliga för teckensnittsfärgen. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Fyllningsfärg </td> 
   <td colname="2"> <p>Färgen på bakgrunden i det fönster där texten finns. </p> <p>Kan ställas in på något av de värden som är tillgängliga för teckensnittsfärgen. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Ogenomskinlighet för teckensnitt </td> 
   <td colname="2"> <p>Textens opacitet. </p> <p>Uttryckt som en procentandel från 0 (helt genomskinlig) till 100 (helt ogenomskinlig). <span class="codeph"> DEFAULT_OPACITY  </span> för teckensnittet är 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Bakgrundsopacitet </td> 
   <td colname="2"> <p>Opaciteten för bakgrundsteckencellen. </p> <p>Uttryckt som en procentandel från 0 (helt genomskinlig) till 100 (helt ogenomskinlig). <span class="codeph"> DEFAULT_OPACITY  </span> för bakgrunden är 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Fyllningsopacitet </td> 
   <td colname="2"> <p>Opaciteten för bildtextfönstrets bakgrund. </p> <p>Uttryckt som en procentandel från 0 (helt genomskinlig) till 100 (helt ogenomskinlig). <span class="codeph"> DEFAULT_OPACITY  </span> för fill är 0. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Exempel på bildtextformatering {#examples-caption-formatting}

Du kan ange textningsformat.

**Exempel 1: Ange formatvärden explicit**

```java
private final MediaPlayer.PlaybackEventListener  
  _playbackEventListener = new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // Set CC style. 
        TextFormat tf = new TextFormatBuilder(TextFormat.Font.DEFAULT, 
        TextFormat.Size.DEFAULT, 
        TextFormat.FontEdge.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.DEFAULT_OPACITY, 
        TextFormat.DEFAULT_OPACITY, 
        TextFormat.DEFAULT_OPACITY).toTextFormat(); 
        mediaPlayer.setCCStyle(tf); 
        ... 
    } 
} 
```

**Exempel 2: Ange formatvärden i parametrar**

```java
/** 
* Constructor using parameters to initialize a TextFormat. 
* 
* @param font 
* The desired font. 
* @param size 
* The desired text size. 
* @param fontEdge 
* The desired font edge. 
* @param fontColor 
* The desired font color. 
* @param backgroundColor 
* The desired background color. 
* @param fillColor 
* The desired fill color. 
* @param edgeColor 
* The desired color to draw the text edges. 
* @param fontOpacity  
* The desired font opacity. 
* @param backgroundOpacity 
* The desired background opacity. 
* @param fillOpacity 
* The desired fill opacity.  
*/ 
public TextFormatBuilder( 
    Font font, Size size, FontEdge fontEdge, 
    Color fontColor, Color backgroundColor,  
    Color fillColor, Color edgeColor, 
    int fontOpacity, int backgroundOpacity, 
    int fillOpacity); 
 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public TextFormat toTextFormat(); 
 
/** 
* Sets the text font. 
* @param font The desired font 
* @return This builder object to allow chaining calls 
*/ 
public TextFormatBuilder setFont(Font font); 
... 
```
