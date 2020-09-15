---
description: Du kan ange formatinformation för textningsspår med klassen TextFormat som anger formatet för textning som visas av spelaren.
seo-description: Du kan ange formatinformation för textningsspår med klassen TextFormat som anger formatet för textning som visas av spelaren.
seo-title: Styr textningsformat
title: Styr textningsformat
uuid: fa4f637f-f13c-465d-8eee-5e66a6dd9db2
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---


# Styr textningsformat {#control-closed-caption-styling}

Du kan ange formatinformation för textningsspår med klassen TextFormat som anger formatet för textning som visas av spelaren.

Den här klassen kapslar in formatinformation för undertexter som teckensnittstyp, storlek, färg och bakgrundsopacitet.

## Ange format för undertexter {#section_C9B5E75C70DD42E59DC4DD0F308C8216}

Du kan formatera undertexttexten med TVSDK-metoder.

1. Vänta tills mediespelaren har minst `PREPARED` status.
1. Skapa en `TextFormatBuilder` instans.

   Du kan ange alla parametrar för textningsformat nu eller ange dem senare.

   TVSDK kapslar in formatinformation för undertexter i `TextFormat` gränssnittet. Klassen skapar `TextFormatBuilder` objekt som implementerar det här gränssnittet.

   ```java
   public TextFormatBuilder( 
      TextFormat.Font font, 
      TextFormat.Size size, 
      TextFormat.FontEdge fontEdge, 
      java.lang.String fontColor, 
      java.lang.String backgroundColor, 
      java.lang.String fillColor, 
      java.lang.String edgeColor, 
      int fontOpacity, 
      int backgroundOpacity, 
      int fillOpacity 
      java.lang.String bottomInset, 
      java.lang.String safeArea)
   ```

1. Om du vill hämta en referens till ett objekt som implementerar `TextFormat` gränssnittet anropar du metoden `TextFormatBuilder.toTextFormat` public.

   >[!NOTE]
   >
   >Detta returnerar ett `TextFormat` objekt som kan tillämpas på mediespelaren.

   ```java
   public TextFormat toTextFormat()
   ```

1. Du kan även hämta de aktuella stilinställningarna för undertextning genom att göra något av följande:

   * Hämta alla formatinställningar med returvärdet är `MediaPlayer.getCCStyle` en instans av `TextFormat` gränssnittet.

      ```java
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws MediaPlayerException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws MediaPlayerException;
      ```

   * Hämta inställningarna en åt gången med hjälp av `TextFormat` gränssnittets get-metoder.

      ```java
      public java.lang.String getFontColor(); 
      public java.lang.String getBackgroundColor(); 
      public java.lang.String getFillColor(); // retrieve the font fill color 
      public java.lang.String getEdgeColor(); // retrieve the font edge color 
      public TextFormat.Size getSize(); // retrieve the font size 
      public TextFormat.FontEdge getFontEdge(); // retrieve the font edge type 
      public TextFormat.Font getFont(); // retrieve the font type 
      public int getFontOpacity(); 
      public int getBackgroundOpacity(); 
      public java.lang.String getBottomInset(java.lang.String bi); 
      public java.lang.String getSafeArea(java.lang.String sa);
      ```

1. Gör något av följande om du vill ändra formatinställningarna:

   * Använd metoden set `MediaPlayer.setCCStyle`och skicka en instans av `TextFormat` gränssnittet:

      ```java
      /** 
      * Sets the closed captioning style. Used to control the closed captioning font, 
      * size, color, edge and opacity.  
      * 
      * This method is safe to use even if the current media stream doesn't have closed 
      * captions. 
      * 
      * @param textFormat 
      * @throws MediaPlayerException 
      */ 
      public void setCCStyle(TextFormat textFormat) throws MediaPlayerException;
      ```

   * Använd klassen `TextFormatBuilder` som definierar enskilda set-metoder.

      Gränssnittet definierar ett objekt som inte kan ändras, så det finns bara get-metoder och inga set-metoder. `TextFormat` Du kan bara ange parametrar för textningsformat med `TextFormatBuilder` klassen:

      ```java
      // set font type 
      public void setFont(Font font)  
      public void setBackgroundColor(String backgroundColor) 
      public void setFillColor(String fillColor) 
      // set the font-edge color 
      public void setEdgeColor(String edgeColor)  
      // set the font size 
      public void setSize(Size size)  
      // set the font edge type 
      public void setFontEdge(FontEdge fontEdge)  
      public void setFontOpacity(int fontOpacity) 
      public void setBackgroundOpacity(int backgroundOpacity) 
      // set the font-fill opacity level 
      public void setFillOpacity(int fillOpacity)  
      public void setFontColor(String fontColor) 
      public void setBottomInset(String bi) 
      public void setSafeArea(String sa) 
      public void setTreatSpaceAsAlphaNum(bool)
      ```

      >[!IMPORTANT]
      >
      >**Färginställningar:** I Android TVSDK 2.X har färgstilen för undertexter förbättrats. Förbättringen gör det möjligt att ställa in undertextningsfärger med en hexadecimal sträng som representerar RGB-färgvärden. RGB hex-färgåtergivningen är den välkända 6 byte-strängen som du använder i program som Photoshop:
      >
      >    * FFFFFF = Svart
      >    * 000000 = Vit
      >    * FF0000 = röd
      >    * 00FF00 = Grön
      >    * 0000FF = Blå

      >
      >och så vidare.
      >
      >När du skickar färgformatsinformation till `TextFormatBuilder`programmet använder du uppräkningen som tidigare, men nu måste du lägga `Color` `getValue()` till färgen för att få värdet som en sträng. Exempel:

      ```
      tfb = tfb.setBackgroundColor(TextFormat.Color.RED <b>.getValue()</b>);
      ```




Att ställa in stilen för undertexter är en asynkron åtgärd, så det kan ta upp till några sekunder innan ändringarna visas på skärmen.

## Alternativ för textningsformat {#section_6D685EC2D58C42A2BDDD574EDFCCC2A0}

Du kan ange flera alternativ för bildtextformat och de här alternativen åsidosätter formatalternativen i de ursprungliga bildtexterna.

```java
public TextFormatBuilder( 
   Font font, 
   Size size, 
   FontEdge fontEdge, 
   String fontColor, 
   String backgroundColor, 
   String fillColor, 
   String edgeColor, 
   int fontOpacity, 
   int backgroundOpacity, 
   int fillOpacity,  
   String bottomInset 
   String safeArea)
```

>[!TIP]
I alternativ som definierar standardvärden (till exempel `DEFAULT`) refererar det värdet till inställningen som var när bildtexten ursprungligen angavs.

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Format </th> 
   <th colname="2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> Teckensnitt </td> 
   <td colname="2"> <p>Teckensnittstypen. </p> <p>Kan bara anges till ett värde som definieras av <span class="codeph"> </span> uppräkningen TextFormat.Font och representerar t.ex. fast teckenbredd med eller utan serifer. </p> <p>Tips:  De faktiska teckensnitten som finns på en enhet kan variera, och ersättningar används vid behov. Monospace med serifer används vanligtvis som ersättning, men den här ersättningen kan vara systemspecifik. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Storlek </td> 
   <td colname="2"> <p>Bildtextens storlek. </p> <p> Kan endast anges till ett värde som definieras av <span class="codeph"> uppräkningen TextFormat.Size </span> : 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MEDIUM </span> - Standardstorlek </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> STOR </span> - cirka 30 % större än mediet </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> SMALL </span> - Cirka 30 % mindre än medium </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> STANDARD </span> - Bildtextens standardstorlek; samma som medium </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Teckensnittskant </td> 
   <td colname="2"> <p>Den effekt som används för teckensnittskanten, till exempel upphöjd eller ingen. </p> <p>Kan bara anges till ett värde som definieras av <span class="codeph"> uppräkningen TextFormat.FontEdge </span> . </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Teckenfärg </td> 
   <td colname="2"> <p>Teckenfärgen. </p> <p>Kan endast anges till ett värde som definieras av <span class="codeph"> TextFormat.Color- </span> uppräkningen. </p> </td> 
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
   <td colname="2"> <p>Textens opacitet. </p> <p>Uttryckt som en procentandel från 0 (helt genomskinlig) till 100 (helt ogenomskinlig). <span class="codeph"> DEFAULT_OPACITY </span> för teckensnittet är 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Bakgrundsopacitet </td> 
   <td colname="2"> <p>Opaciteten för bakgrundsteckencellen. </p> <p>Uttryckt som en procentandel från 0 (helt genomskinlig) till 100 (helt ogenomskinlig). <span class="codeph"> DEFAULT_OPACITY </span> för bakgrunden är 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Fyllningsopacitet </td> 
   <td colname="2"> <p>Opaciteten för bildtextfönstrets bakgrund. </p> <p>Uttryckt som en procentandel från 0 (helt genomskinlig) till 100 (helt ogenomskinlig). <span class="codeph"> DEFAULT_OPACITY </span> för fill är 0. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Undre indrag </td> 
   <td colname="2"> <p>Lodrätt avstånd från underkanten av bildtextfönstret för bildtexter som ska undvikas. </p> <p>Uttrycks som en procentandel av bildtextfönstrets höjd (till exempel "20%") eller ett antal pixlar (till exempel "20"). </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> Säkert område </td> 
   <td colname="2"> <p>Ett område runt skärmens kant på mellan 0 % och 25 % där bildtexter inte visas. </p> <p>Som standard är det säkra området för WebVTT 0 %. Med den här inställningen kan programmet åsidosätta den standardinställningen. Om två värden anges, till exempel strängen "10%,20%", är det första värdet det vågräta säkra området och det andra värdet det lodräta säkra området. Om ett värde anges, till exempel strängen "15%", används det angivna säkra området både för den lodräta och vågräta axeln. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Exempel på bildtextformatering {#section_58E8E82494EC4683B010FFDE67485CF9}

Här är några exempel som visar hur du anger formatering för undertexter.

**Exempel 1: Ange formatvärden explicit**

```java
private final MediaPlayer.PlaybackEventListener _playbackEventListener = 
  new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // Set CC style. 
        TextFormat tf = new TextFormatBuilder( 
            TextFormat.Font.DEFAULT, 
            TextFormat.Size.DEFAULT, 
            TextFormat.FontEdge.DEFAULT, 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
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
public  
<b>TextFormatBuilder</b>( 
    Font font, Size size, FontEdge fontEdge, 
    String fontColor, String backgroundColor,  
    String fillColor, String edgeColor, 
    int fontOpacity, int backgroundOpacity, 
    int fillOpacity); 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public TextFormat  
<b>toTextFormat</b>(); 
/** 
* Sets the text font. 
* @param font The desired font 
* @return This builder object to allow chaining calls 
*/ 
public  
<b>TextFormatBuilder</b> setFont(Font font); 
...
```
