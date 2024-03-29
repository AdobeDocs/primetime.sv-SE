---
description: PTMediaPlayer-objektet representerar din mediespelare. Ett PTMediaPlayerItem representerar ljud eller video i spelaren.
title: Arbeta med MediaPlayer-objekt
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Arbeta med MediaPlayer-objekt{#work-with-mediaplayer-objects}

PTMediaPlayer-objektet representerar din mediespelare. Ett PTMediaPlayerItem representerar ljud eller video i spelaren.

## Om klassen MediaPlayerItem {#section_B6F36C0462644F5C932C8AA2F6827071}

När en medieresurs har lästs in, skapar TVSDK en instans av `PTMediaPlayerItem` klass som ger åtkomst till den resursen.

The `PTMediaPlayer` löser medieresursen, läser in den associerade manifestfilen och tolkar manifestet. Detta är den asynkrona delen av resursinläsningsprocessen. The `PTMediaPlayerItem` -instansen skapas när resursen har lösts och den här instansen är en löst version av en medieresurs. TVSDK ger åtkomst till nyskapade `PTMediaPlayerItem` instansen through `PTMediaPlayer.currentItem`.

>[!TIP]
>
>Du måste vänta tills resursen har lästs in innan du kan komma åt mediespelarobjektet.

## MediaPlayer-objektets livscykel {#section_D87EF7FBC7B442BDBE825156DC2C1CCF}

Från det ögonblick du skapar `PTMediaPlayer` till den tidpunkt då du avslutar (återanvänder eller tar bort) den här instansen avslutar en serie övergångar från en status till en annan.

Vissa åtgärder tillåts bara när spelaren är i ett visst läge. Anropa till exempel `play` in `PTMediaPlayerStatusCreated` är inte tillåtet. Du kan bara anropa den här statusen när spelaren når `PTMediaPlayerStatusReady` status.

Så här arbetar du med statusvärden:

* Du kan hämta aktuell status för MediaPlayer-objektet med `PTMediaPlayer.status`.
* Statuslistan definieras i `PTMediaPlayerStatus`.

Delövergångsdiagram för livscykeln för en MediaPlayer-instans:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-ios2_web.png)

I följande tabell finns mer information:

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> PTMediaPlayerStatus </th> 
   <th colname="col2" class="entry"> Inträffar när </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusSkapad</span> </p> </td> 
   <td colname="col2"> <p>Programmet begärde en ny mediespelare genom att ringa <span class="codeph"> playerWithMediaPlayerItem</span>. Den nya spelaren väntar på att du ska ange ett mediespelarobjekt. Detta är mediespelarens ursprungliga status. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusInitializing</span> </p> </td> 
   <td colname="col2"> <p>Dina programsamtal <span class="codeph"> PTMediaPlayer.replaceCurrentItemWithPlayerItem</span>och mediespelaren läses in. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusInitialized</span> </p> </td> 
   <td colname="col2"> <p>TVSDK har angett mediespelarobjektet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusReady</span> </p> </td> 
   <td colname="col2"> <p>Innehållet förbereds och annonser har infogats på tidslinjen, eller så misslyckades annonseringsproceduren. Buffring eller uppspelning kan börja. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusSpela upp</span> </p> </td> 
   <td colname="col2"> <p>Ditt program har anropat <span class="codeph"> play</span>så TVSDK försöker spela upp videon. Viss buffring kan inträffa innan videon spelas upp. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPaused</span> </p> </td> 
   <td colname="col2"> <p>När ditt program spelar upp och pausar media flyttas mediespelaren mellan det här läget och <span class="codeph"> PTMediaPlayerStatusSpela upp</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusSlutförd</span> </p> </td> 
   <td colname="col2"> <p>Spelaren har nått slutet av strömmen och uppspelningen har stoppats. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusStoppad</span> </p> </td> 
   <td colname="col2"> <p>Ditt program har släppt mediespelaren, som också frigör associerade resurser. Du kan inte längre använda den här instansen </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusError</span> </p> </td> 
   <td colname="col2"> <p>Ett fel uppstod under processen. Ett fel kan också påverka vad ditt program kan göra härnäst. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Du kan använda statusen för att ge feedback om processen (till exempel en snurra som väntar på nästa statusändring) eller för att utföra nästa steg i uppspelningen av media, till exempel vänta på rätt status innan du anropar nästa metod.
