---
description: Programmet kan övervaka aktiviteten i spelaren och spelarens föränderliga tillstånd genom att avlyssna händelser som skickas av TVSDK.
title: Uppspelningshändelser
exl-id: 9fb77b57-be6c-4dab-b779-d8c606938e46
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# Uppspelningshändelser {#playback-events}

Programmet kan övervaka aktiviteten i spelaren och spelarens föränderliga tillstånd genom att avlyssna händelser som skickas av TVSDK.

TVSDK skickar uppspelningshändelser när medieuppspelningsåtgärder utförs, till exempel när en video börjar spelas upp. Om du vill få meddelanden om alla uppspelningsrelaterade händelser registrerar du avlyssnare med `MediaPlayer` -objekt för följande händelser.

<table frame="all" colsep="1" rowsep="1" id="table_922EEA3DE0BD47BA982E11F890CA0A6B"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Händelse </th> 
   <th colname="2" class="entry"> Betydelse </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>Uppspelning</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_SELECTED" format="html" scope="external"> RATE_SELECTED</a> </td> 
   <td colname="2"> Användaren eller TVSDK har valt en ny uppspelningshastighet, till exempel snabb framåt, bakåt eller återuppta uppspelning med normal hastighet. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_PLAYING" format="html" scope="external"> RATE_PLAYING</a> </td> 
   <td colname="2"> En ny uppspelningshastighet visas på skärmen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> TimeChangeEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html#TIME_CHANGED" format="html" scope="external"> TIME_CHANGED</a> </td> 
   <td colname="2"> Mediets aktuella spelhuvudposition har ändrats. Skickas periodiskt när den aktuella tiden har ändrats, var 250:e ms eller mer. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Media Player</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerStatus ChangeEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html#STATUS_CHANGED" format="html" scope="external"> STATUS_CHANGED</a> </td> 
   <td colname="2"> Mediespelarens status har ändrats. Programmet bör hantera fel i den här händelsens återanrop. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">ProfileEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html#PROFILE_CHANGED" format="html" scope="external"> PROFILE_CHANGED</a> </td> 
   <td colname="2">Mediespelarens aktuella profil har ändrats. Använd <span class="codeph"> ProfileEvent.profile</span> för att hämta den nya profilen som spelas upp. Använd <span class="codeph"> tid</span> för att hämta tiden när den här händelsen inträffade. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>MediaplayerItem</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem-händelse.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_CREATED" format="html" scope="external"> ITEM_CREATED</a> </td> 
   <td colname="2">A <span class="codeph"> MediaPlayerItem</span> har skapats. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem-händelse.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_UPDATED" format="html" scope="external"> ITEM_UPDATED</a> </td> 
   <td colname="2">Mediespelaren har uppdaterat mediet i något av följande fall: 
    <ul id="ul_E4D1A1D468544C3B9F8046E9B68A956D"> 
     <li id="li_35A2A417BF924E039D9CB36CFBCDFEB6">När en manifestuppdatering inträffar för en liveresurs. </li> 
     <li id="li_E7AB380C212B4011B07C3B313282681C">När en VOD eller en liveresurs har en undertextning och aktivitet för första gången identifieras för ett undertextningsspår. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Bildtexter och ljud</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> MediaPlayerItem-händelse.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#CAPTION_UPDATED" format="html" scope="external"> CAPTION_UPDATED</a> </td> 
   <td colname="2">Ett nytt textningsspår har identifierats i medieströmmen och <span class="codeph"> closedCaptionsTracks</span> samlingen har uppdaterats. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Manifest och Timeline</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="0"> 
   <td colname="1">TimelineEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED" format="html" scope="external"> TIMELINE_UPDATED</a> </td> 
   <td colname="2">Mediespelaren har lagt till eller tagit bort annonser, så den har en uppdaterad tidslinje. <p>Det manifest som uppdaterats för en livedatabas och gamla annonsbrytningar togs bort från tidslinjen eller så upptäcktes nya annonsmöjligheter (referenspunkter). Mediespelaren försöker lösa och placera nya annonser på tidslinjen. </p> <p> Använd den här händelsen för att kontrollera om tidslinjen har några uppdateringar (VOD ändras inte under uppspelning). Sedan kan du hämta tidslinjen med <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html#timeline" format="html" scope="external"> MediaPlayer.timeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
