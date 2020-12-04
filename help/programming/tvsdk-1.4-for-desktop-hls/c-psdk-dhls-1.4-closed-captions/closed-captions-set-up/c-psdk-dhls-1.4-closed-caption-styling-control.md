---
description: Du kan ange formatinformation för textningsspår med klassen ClosedCaptionStyles. Detta anger formatet för alla undertexter som visas av spelaren.
seo-description: Du kan ange formatinformation för textningsspår med klassen ClosedCaptionStyles. Detta anger formatet för alla undertexter som visas av spelaren.
seo-title: Styr textningsformat
title: Styr textningsformat
uuid: 506c06d3-8fe0-46c9-9ed6-5b35d21c021c
translation-type: tm+mt
source-git-commit: b67a9dcb0abb07f4fdff4e03d9d6c0b07ff45127
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 0%

---


# Kontrollera textningsformat för undertexter{#control-closed-caption-styling}

Du kan ange formatinformation för textningsspår med klassen ClosedCaptionStyles. Detta anger formatet för alla undertexter som visas av spelaren.

Den här klassen kapslar in formatinformation för undertexter som teckensnittstyp, storlek, färg och bakgrundsopacitet. En associerad hjälpklass, `ClosedCaptionStylesBuilder`, underlättar arbetet med formatinställningar för undertexter.

## Ange format för undertexter {#section_DAE84659D1964DB1B518F91B59AF29D9}

Du kan formatera undertexttexten med TVSDK-metoder.

1. Vänta tills MediaPlayer har minst statusen PREPARED (se [Vänta på ett giltigt tillstånd](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-state-prepared-wait-for.md)).
1. Gör något av följande om du vill ändra formatinställningarna:

   * Använd hjälpklassen `ClosedCaptionStylesBuilder` (används i `ClosedCaptionStyles` bakom scenerna).
   * Använd klassen `ClosedCaptionStyles` direkt.

>[!NOTE]
>
>Att ställa in stilen för undertexter är en asynkron åtgärd så det kan ta upp till några sekunder innan ändringarna visas på skärmen.

## Alternativ för textningsformat {#section_D28F50B98C0D48CF89C4FB6DC81C5185}

Du kan ange formatinformation för textningsspår med klassen `ClosedCaptionStyles`. Detta anger formatet för alla undertexter som visas av spelaren.

```
public function TextFormat( 
   font:String = default,  
   size:String = default,  
   fontEdge:String = default,  
   fontColor:String = default,  
   backgroundColor:String = default,  
   fillColor:String = default,  
   edgeColor:String = default,  
   fontOpacity:int,  
   backgroundOpacity:int,  
   fillOpacity:int)
```

>[!TIP]
>
>I alternativ som definierar standardvärden (till exempel `DEFAULT`) refererar det värdet till inställningen som var när bildtexten ursprungligen angavs.

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
   <td colname="2"> <p>Teckensnittstypen. </p> <p>Kan endast anges till ett värde som definieras av matrisen <span class="codeph"> ClosedCaptionStyles.FONT </span> och representerar till exempel fast teckenbredd med eller utan serifer. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;FONT&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;AVCaptionStyle.MONOSPACE_WITH_SERIFS, 
      &nbsp;AVCaptionStyle.MONOSPACED_WITHOUT_SERIFS, 
      &nbsp;AVCaptionStyle.PROPORTIONAL_WITH_SERIFS, 
      &nbsp;AVCaptionStyle.PROPORTIONAL_WITHOUT_SERIFS, 
      &nbsp;AVCaptionStyle.CASUAL, 
      &nbsp;AVCaptionStyle.CURSIVE, 
      &nbsp;AVCaptionStyle.SMALL_CAPITALS 
      &nbsp;]; 
     </code> </p> <p>Tips:  De faktiska teckensnitten som finns på en enhet kan variera, och ersättningar används vid behov. Monospace med serifer används vanligtvis som ersättning, men den här ersättningen kan vara systemspecifik. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Storlek </td> 
   <td colname="2"> <p>Bildtextens storlek. </p> <p> Kan endast anges till ett värde som definieras av <span class="codeph">-matrisen ClosedCaptionStyles.FONT_SIZE </span>: 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MEDIUM  </span> - Standardstorlek </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> STOR  </span> - Cirka 30 % större än mediet </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> SMALL  </span> - Cirka 30 % mindre än medium </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> STANDARD  </span> - Bildtextens standardstorlek; samma som medium </li> 
     </ul> </p> <p>Tips:  Du kan ändra teckenstorleken för WebVTT-bildtexter genom att ändra parametern size för funktionen <span class="codeph"> DefaultMediaPlayer.ccStyles setter </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Teckensnittskant </td> 
   <td colname="2"> <p>Den effekt som används för teckensnittskanten, till exempel upphöjd eller ingen. </p> <p>Kan endast anges till ett värde som definieras av matrisen <span class="codeph"> ClosedCaptionStyles.FONT_EDGE </span>. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;FONT_EDGE&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.NONE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RAISED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEPRESSED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.UNIFORM, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.LEFT_DROP_SHADOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RIGHT_DROP_SHADOW 
      &nbsp;]; 
     </code> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Teckenfärg </td> 
   <td colname="2"> <p>Teckenfärgen. </p> <p>Kan endast anges till ett värde som definieras av matrisen <span class="codeph"> ClosedCaptionStyles.COLOR </span>. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;COLOR&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BLACK, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.GRAY, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.WHITE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_WHITE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.CYAN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_CYAN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_CYAN&nbsp;&nbsp;&nbsp;]; 
     </code> </p> </td> 
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
   <td colname="2"> <p>Färgen på bakgrunden i det fönster där texten finns. </p> <p>Kan ställas in på något av de värden som är tillgängliga för teckensnittsfärgen. </p> <p>Viktigt:  Detta gäller inte WebVTT-bildtexter eftersom WebVTT inte använder den här funktionen. </p> </td> 
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

## Exempel: Bildtextformatering {#section_63E33840B7A14D26990046E2ACF2ECA1}

Du kan ange textningsformat.

## Exempel 1: Ange formatvärden explicit {#section_BD7B48F3B66D4E9290E1CB2F464E08E4}

```
private function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    var formatBuilder:TextFormatBuilder = new TextFormatBuilder(); 
    formatBuilder.font = Font.DEFAULT,  
    formatBuilder.fontSize = FontSize.DEFAULT,  
    formatBuilder.fontEdge = FontEdge.DEFAULT,  
    formatBuilder.fontColor = Color.DEFAULT,  
    formatBuilder.backgroundColor = Color.DEFAULT,  
    formatBuilder.fillColor = Color.DEFAULT,  
    formatBuilder.edgeColor = Color.DEFAULT,  
    formatBuilder.fontOpacity = .DEFAULT_OPACITY,  
    formatBuilder.backgroundOpacity = Font.DEFAULT_OPACITY,  
    formatBuilder.fillOpacity = TextFormat.DEFAULT_OPACITY 
    mediaPlayer.set CCStyle(formatBuilder.toTextFormat()); 
} 
```

## Exempel 2: Ange formatvärden i parametrar {#section_147036D7C31C4010A5A7DF49997014A9}

```
/** 
* Constructor using parameters to initialize a TextFormat. 
* 
* @param font 
* The desired font. 
* @param fontSize 
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
public function TextFormatBuilder(font:Font, fontSize:FontSize, fontEdge:FontEdge,  
                                  fontColor:Color, backgroundColor:Color,  
                                  fillColor:Color, edgeColor:Color, fontOpacity:int, 
                                  backgroundOpacity:int, fillOpacity:int); 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public function toTextFormat():TextFormat; 
... 
```
