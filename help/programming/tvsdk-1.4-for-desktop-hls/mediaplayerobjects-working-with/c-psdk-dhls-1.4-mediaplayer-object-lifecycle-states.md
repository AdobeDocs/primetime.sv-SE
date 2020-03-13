---
description: Från den stund du skapar MediaPlayer-instansen till den tidpunkt då du avslutar (återanvänder eller tar bort) den, slutförs en serie övergångar mellan statusarna.
seo-description: Från den stund du skapar MediaPlayer-instansen till den tidpunkt då du avslutar (återanvänder eller tar bort) den, slutförs en serie övergångar mellan statusarna.
seo-title: MediaPlayer-objektets livscykel
title: MediaPlayer-objektets livscykel
uuid: 1452ae3a-7ce9-439e-951c-9d3db63b1d20
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# MediaPlayer-objektets livscykel{#mediaplayer-object-lifecycle}

Från den stund du skapar MediaPlayer-instansen till den tidpunkt då du avslutar (återanvänder eller tar bort) den, slutförs en serie övergångar mellan statusarna.

Vissa åtgärder tillåts bara när spelaren är i ett visst läge. Anrop `play` i IDLE är till exempel inte tillåtet. Du kan bara anropa den här statusen efter att spelaren har nått tillståndet PREPARED.

Så här arbetar du med status:

* Du kan hämta det aktuella läget för `MediaPlayer` objektet med hjälp av `MediaPlayer.status` egenskapen.

   ```
   function get status():String;
   ```

* Statuslistan definieras i `MediaPlayer.PlayerStatus`.

Diagram över övergång av en `MediaPlayer` instans livscykel:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-flash-1_2_web.png)

I följande tabell finns mer information:

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <span class="codeph"> MediaPlayerStatus </span> </th> 
   <th colname="col2" class="entry"> Inträffar när </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> IDLE </span> </td> 
   <td colname="col2"> <p> Programmet begärde en ny mediespelare genom att initiera <span class="codeph"> MediaPlayer </span>. Den nya spelaren väntar på att du ska ange ett mediespelarobjekt. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INITIERAR </span> </td> 
   <td colname="col2"> <p>Programmet <span class="codeph"> MediaPlayer.replaceCurrentResource </span>och mediespelaren läses in. </p> </td> 
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
   <td colname="col1"> <span class="codeph"> SÖKER </span> </td> 
   <td colname="col2"> <p>Mediespelaren försöker hitta rätt position när den pausas eller spelas upp. Avlyssna händelserna SeekEvent.SEEK_BEGIN <span class="codeph"> och </span> <span class="codeph"> </span> SeekEvent.SEEK_END för att avgöra när sökningen har påbörjats eller avslutats. </p> </td> 
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
>Du kan använda statusen för att ge feedback om processen (till exempel en snurra som väntar på nästa statusändring) eller för att utföra nästa steg i uppspelningen av media, till exempel vänta på rätt status innan du anropar nästa metod.

