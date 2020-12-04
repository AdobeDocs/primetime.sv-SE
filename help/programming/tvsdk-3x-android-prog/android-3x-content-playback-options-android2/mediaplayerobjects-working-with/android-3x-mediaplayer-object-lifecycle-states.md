---
description: Mediespelarens status avgör vilka åtgärder som är giltiga.
seo-description: Mediespelarens status avgör vilka åtgärder som är giltiga.
seo-title: Livscykel och status för MediaPlayer-objektet
title: Livscykel och status för MediaPlayer-objektet
uuid: a2866f84-a722-46ed-b4cb-36664db5be82
translation-type: tm+mt
source-git-commit: 56dc79e5b4df11ff730d7d8f23dea8d0f4712077
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---


# Livscykel och status för MediaPlayer-objektet{#lifecycle-and-statuses-of-the-mediaplayer-object}

Mediespelarens status avgör vilka åtgärder som är giltiga.

För att arbeta med status för mediespelare:

* Du kan hämta aktuell status för `MediaPlayer`-objektet med `MediaPlayer.getStatus()`.

* Statuslistan definieras i uppräkningen [MediaPlayerStatus](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/com/adobe/mediacore/MediaPlayerStatus.html).

Statusövergångsdiagram för livscykeln för en `MediaPlayer`-instans:

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
   <td colname="col2"> <p>Ditt program anropar <span class="codeph"> MediaPlayer.replaceCurrentItem() </span>. </p> <p>Mediespelarobjektet läses in. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> INITIERAD </td> 
   <td colname="col2"> <p>TVSDK har angett mediespelarobjektet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> FÖRBEREDER </td> 
   <td colname="col2"> <p>Ditt program anropar <span class="codeph"> MediaPlayer.prepareToPlay() </span>. Mediespelaren läser in mediespelarobjektet och associerade resurser. </p> </td> 
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
   <td colname="col2"> <p>Om programmet navigerar bort från uppspelningen, stänger av enheten eller växlar program medan spelaren spelas upp eller pausas, pausas mediespelaren och resurser frigörs. </p> <p>Om du anropar <span class="codeph"> MediaPlayer.restore() </span> återställs spelaren till den status som spelaren hade innan den SUSPENDED användes. Undantaget är om spelaren SEEKING anropas när den pausas, PAUSED och sedan SUSPENDED. </p> <p>Viktigt:  <p>Kom ihåg följande information: 
      <ul id="ul_1B21668994D1474AAA0BE839E0D69B00"> 
       <li id="li_08459A3AB03C45588D73FA162C27A56C">Med <span class="codeph"> MediaPlayer </span> anropas automatiskt <span class="codeph"> paus </span> bara när det ytobjekt som används av MediaPlayerView </span> förstörs.<span class="codeph"> </span></li> 
       <li id="li_B9926AA2E7B9441490F37D24AE2678A1"><span class="codeph"> MediaPlayer </span> anropar automatiskt <span class="codeph"> restore() </span> bara när ett nytt ytobjekt som används av MediaPlayerView </span> skapas.<span class="codeph"> </span></li> 
      </ul> </p> </p> <p>Om du alltid vill att uppspelningen ska pausas när MediaPlayer återställs ska du låta programmet anropa <span class="codeph"> MediaPlayer.pause() </span> i Android-aktivitetens <span class="codeph"> onPause() </span>-metod. </p> </td> 
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

Exempel:

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
