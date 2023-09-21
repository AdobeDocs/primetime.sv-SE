---
description: Mediespelarens status avgör vilka åtgärder som är giltiga.
title: Livscykel och status för MediaPlayer-objektet
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# Livscykel och status för MediaPlayer-objektet{#lifecycle-and-statuses-of-the-mediaplayer-object}

Mediespelarens status avgör vilka åtgärder som är giltiga.

För att arbeta med status för mediespelare:

* Du kan hämta aktuell status för `MediaPlayer` objekt med `MediaPlayer.getStatus()`.

* Statuslistan definieras i [MediaPlayerStatus](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/com/adobe/mediacore/MediaPlayerStatus.html) enum.

Statusövergångsdiagram för livscykeln för en `MediaPlayer` instans:

<!--<a id="fig_A6425F24C7734DC681D992859D2A6743"></a>-->

![](assets/media_player_statuses.png)

Följande tabell innehåller information om mediespelarens livscykel och status:

<table id="table_82757A0043EB4AACA474E6B30326A6B7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Status </th> 
   <th colname="col2" class="entry"> Inträffar när </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> IDLE </td> 
   <td colname="col2"> <p>Mediespelarens ursprungliga status. Spelaren skapas och väntar på att du ska ange ett mediespelarobjekt. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> INITIERAR </td> 
   <td colname="col2"> <p>Dina programsamtal <span class="codeph"> MediaPlayer.replaceCurrentItem() </span>. </p> <p>Mediespelarobjektet läses in. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> INITIERAD </td> 
   <td colname="col2"> <p>TVSDK har angett mediespelarobjektet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> FÖRBEREDER </td> 
   <td colname="col2"> <p>Dina programsamtal <span class="codeph"> MediaPlayer.prepareToPlay() </span>. Mediespelaren läser in mediespelarobjektet och associerade resurser. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> FÖRBEREDD </td> 
   <td colname="col2"> <p>TVSDK har förberett medieströmmen och har försökt att utföra annonsupplösning och annonsinfogning (om det är aktiverat). Innehållet förbereds och annonser har infogats på tidslinjen, eller så misslyckades annonseringsproceduren. </p> <p>Buffring eller uppspelning kan börja. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> SPELA UPP/PAUSAS </td> 
   <td colname="col2"> <p>När programmet spelar upp och pausar media flyttas mediespelaren mellan dessa lägen. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> UPPHÄVD </td> 
   <td colname="col2"> <p>Om programmet navigerar bort från uppspelningen, stänger av enheten eller växlar program medan spelaren spelas upp eller pausas, pausas mediespelaren och resurser frigörs. </p> <p>Anropar <span class="codeph"> MediaPlayer.restore() </span> återställer spelaren till den status som spelaren hade innan den SUSPENDED. Undantaget är om spelaren SEEKING anropas när den pausas, PAUSED och sedan SUSPENDED. </p> <p>Viktigt:  <p>Kom ihåg följande information: 
      <ul id="ul_1B21668994D1474AAA0BE839E0D69B00"> 
       <li id="li_08459A3AB03C45588D73FA162C27A56C">The <span class="codeph"> MediaPlayer </span> anrop automatiskt <span class="codeph"> pausa </span> bara när det ytobjekt som används av <span class="codeph"> MediaPlayerView </span> förstörs. </li> 
       <li id="li_B9926AA2E7B9441490F37D24AE2678A1">The <span class="codeph"> MediaPlayer </span> anrop automatiskt <span class="codeph"> restore() </span> bara när ett nytt ytobjekt som används av <span class="codeph"> MediaPlayerView </span> skapas. </li> 
      </ul> </p> </p> <p>Om du alltid vill att uppspelningen ska pausas när MediaPlayer återställs ska du låta programmet ringa <span class="codeph"> MediaPlayer.pause() </span> i Android Activity's <span class="codeph"> onPause() </span> -metod. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> SLUTFÖRD </td> 
   <td colname="col2"> <p>Spelaren har nått slutet av strömmen och uppspelningen har stoppats. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> SLÄPPT </td> 
   <td colname="col2"> <p>Programmet har släppt mediespelaren, som också frigör associerade resurser. Du kan inte längre använda den här instansen. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> FEL </td> 
   <td colname="col2"> <p>Ett fel uppstod under processen. Ett fel kan också påverka vad programmet kan göra härnäst. Mer information finns i <a href="../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-error-handling-set-up.md" format="dita" scope="local"> Konfigurera felhantering </a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Du kan använda statusen för att ge feedback om processen, till exempel en snurra som väntar på nästa statusändring, eller utföra nästa steg när du spelar upp media, till exempel vänta på rätt status innan du anropar nästa metod.

Till exempel:

```java
mediaPlayer.addEventListener(MediaPlayerEvent STATUS_CHANGED, new StatusChangeEventListener() { 
    @Override  
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        switch(event.getStatus()) { 
            case INITIALIZED: 
                mediaPlayer.prepareToPlay(); 
                break; 
            case PREPARING: 
                showBufferingSpinner(); 
                break; 
            case PREPARED: 
                hideBufferingSpinner(); 
                mediaPlayer.play(); 
                break; 
            ...                
        } 
        ... 
    } 
}); 
```
