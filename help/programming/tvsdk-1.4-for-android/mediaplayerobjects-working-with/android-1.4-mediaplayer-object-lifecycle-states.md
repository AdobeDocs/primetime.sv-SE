---
description: Från det ögonblick du skapar MediaPlayer-instansen till det ögonblick du avslutar (återanvänder eller tar bort) den, slutförs en serie övergångar mellan lägen i den här instansen.
seo-description: Från det ögonblick du skapar MediaPlayer-instansen till det ögonblick du avslutar (återanvänder eller tar bort) den, slutförs en serie övergångar mellan lägen i den här instansen.
seo-title: MediaPlayer-objektets livscykel
title: MediaPlayer-objektets livscykel
uuid: 6670a30c-7053-4754-bc36-6bb8590c001d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# MediaPlayer-objektets livscykel{#mediaplayer-object-lifecycle}

Från det ögonblick du skapar MediaPlayer-instansen till det ögonblick du avslutar (återanvänder eller tar bort) den, slutförs en serie övergångar mellan lägen i den här instansen.

Vissa åtgärder tillåts bara när spelaren är i ett visst läge. Anrop `play` till exempel `IDLE` är inte tillåtet. Du kan bara anropa den här statusen när spelaren har nått `PREPARED` läget.

Så här arbetar du med lägen:

* Du kan hämta det aktuella läget för `MediaPlayer` objektet med `MediaPlayer.getStatus`.

   ```java
   PlayerState getStatus() throws IllegalStateException;
   ```

* Listan med lägen definieras i `MediaPlayer.PlayerState`.

Diagram över övergång av en `MediaPlayer` instans livscykel:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

I följande tabell finns mer information:

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> MediaPlayer.PlayerState </th> 
   <th colname="col2" class="entry"> Inträffar när </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> IDLE </span> </td> 
   <td colname="col2"> <p>Programmet begärde en ny mediespelare genom att anropa <span class="codeph"> DefaultMediaPlayer.create </span>. Den nya spelaren väntar på att du ska ange ett mediespelarobjekt. Detta är mediespelarens startläge. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INITIERAR </span> </td> 
   <td colname="col2"> <p>Programmet heter <span class="codeph"> MediaPlayer.replaceCurrentItem </span>och mediespelaren läses in. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INITIERAD </span> </td> 
   <td colname="col2"> <p>TVSDK har angett mediespelarobjektet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> FÖRBEREDER </span> </td> 
   <td colname="col2"> <p>Programmet heter <span class="codeph"> MediaPlayer.prepareToPlay </span>. Mediespelaren läser in mediespelarobjektet och tillhörande resurser. </p> <p>Tips:  En del buffring av huvudmediet kan förekomma. </p> <p>TVSDK förbereder medieströmmen och försöker genomföra annonsupplösning och annonsinfogning (om det är aktiverat). </p> <p>Tips:  Om du vill ställa in starttiden på ett värde som inte är noll anropar du <span class="codeph"> prepareToPlay(startTime) </span> med tiden i millisekunder. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> FÖRBEREDD </span> </td> 
   <td colname="col2"> <p>Innehållet förbereds och annonser har infogats på tidslinjen, eller så misslyckades annonseringsproceduren. Buffring eller uppspelning kan börja. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> SPELA UPP </span> </td> 
   <td colname="col2"> <p>Programmet har anropat <span class="codeph"> play </span>så TVSDK försöker spela upp videon. Viss buffring kan inträffa innan videon spelas upp. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PAUSAT </span> </td> 
   <td colname="col2"> <p>När ditt program spelar upp och pausar media flyttas mediespelaren mellan detta läge och SPELNING. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> UPPHÄVD </span> </td> 
   <td colname="col2"> <p>Ditt program navigerade bort från uppspelningen, stängde av enheten eller växlade program medan spelaren spelades upp eller pausades. Mediespelaren har pausats och resurser har släppts. Återställ mediespelaren för att fortsätta. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> SLUTFÖRD </span> </td> 
   <td colname="col2"> <p>Spelaren har nått slutet av strömmen och uppspelningen har stoppats. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> SLÄPPT </span> </td> 
   <td colname="col2"> <p>Ditt program har släppt mediespelaren, som också frigör associerade resurser. Du kan inte längre använda den här instansen </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> FEL </span> </td> 
   <td colname="col2"> <p>Ett fel uppstod under processen. Ett fel kan också påverka vad ditt program kan göra härnäst. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Du kan använda läget för att ge feedback om processen (till exempel en snurra som väntar på nästa lägesändring) eller för att ta nästa steg i uppspelningen av media, till exempel vänta på rätt läge innan du anropar nästa metod.

Exempel:

```java
@Override 
public void onStateChanged(MediaPlayer.PlayerState state,  
                           MediaPlayerNotification notification) { 
   switch (state) { 
      // It is recommended that you call prepareToPlay() after receiving  
      // the INITIALIZED state. 
      case INITIALIZED: 
         _mediaPlayer.prepareToPlay(); 
         break; 
      case PREPARING: 
         showBufferingSpinner(); 
         break; 
      case PREPARED: 
         hideBufferingSpinner(); 
      ..... 
    } 
}
```

