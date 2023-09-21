---
description: TVSDK skickar uppspelningshändelser när medieuppspelningsåtgärder utförs, till exempel när en video börjar spelas upp.
title: Uppspelningshändelser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# Uppspelningshändelser{#playback-events}

TVSDK skickar uppspelningshändelser när medieuppspelningsåtgärder utförs, till exempel när en video börjar spelas upp.

Registrera en implementering av `MediaPlayer.PlaybackEventListener`, inklusive följande återanrop för händelser.

<table frame="all" colsep="1" rowsep="1"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Händelse </th> 
   <th colname="2" class="entry"> Betydelse </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Uppspelning</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPlayComplete%28%29" format="html" scope="external"> onPlayComplete</a> </td> 
   <td colname="2"> Slutet på en mediekälla har nåtts. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPlayStart%28%29" format="html" scope="external"> onPlayStart</a> </td> 
   <td colname="2"> Uppspelningen av en mediekälla har startat. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onRateSelected%28float%29" format="html" scope="external"> onRateSelected</a> (rörlig ränta) </td> 
   <td colname="2"> Användaren eller TVSDK har valt en ny uppspelningshastighet, till exempel snabb framåt, bakåt eller återuppta uppspelning med normal hastighet. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onRatePlaying%28float%29" format="html" scope="external"> onRatePlaying</a> (rörlig ränta) </td> 
   <td colname="2"> En ny uppspelningshastighet visas på skärmen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Media</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPrepared%28%29" format="html" scope="external"> onFörberedd</a> </td> 
   <td colname="2"> Mediespelaren har förberett mediet. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onSizeAvailable%28long,%20long%29" format="html" scope="external"> onSizeAvailable</a> (lång höjd, lång bredd) </td> 
   <td colname="2"> Mediets storlek är tillgänglig. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Media Player</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onStateChanged%28com.adobe.mediacore.MediaPlayer.PlayerState,com.adobe.mediacore.MediaPlayerNotification%29" format="html" scope="external"> onStateChanged</a> (<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlayerState.html" format="html" scope="external"> MediaPlayer.PlayerState</a> tillstånd, <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html" format="html" scope="external"> MediaPlayerNotification</a> meddelande) </td> 
   <td colname="2"> Mediespelarens tillstånd har ändrats. Programmet bör hantera fel i det här återanropet. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onProfileChanged%28long,%20long%29" format="html" scope="external"> onProfileChanged</a> (lång profil, lång tid) </td> 
   <td colname="2"> Mediespelarens aktuella profil har ändrats. Använd <span class="codeph"> Profil</span> för att hämta den nya profilen som spelas upp. Använd <span class="codeph"> tid</span> för att hämta tiden när den här händelsen inträffade. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>MediaplayerItem</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onUpdated%28%29" format="html" scope="external"> onUpdated</a> </td> 
   <td colname="2">Mediespelaren har uppdaterat mediet i något av följande fall: 
    <ul> 
     <li>När en manifestuppdatering inträffar för en liveresurs.</li> 
     <li>När en VOD eller en liveresurs har en undertextning och aktivitet för första gången identifieras för ett undertextningsspår. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Manifest och Timeline</b></td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimedMetadata%28com.adobe.mediacore.metadata.TimedMetadata%29" format="html" scope="external"> onTimedMetadata</a> (<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html" format="html" scope="external"> TimedMetata</a> timedMetadata) </td> 
   <td colname="2"> En ny tidsbestämd metadata upptäcks i manifestet. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated%28%29" format="html" scope="external"> onTimelineUpdated</a> </td> 
   <td colname="2">Mediespelaren har lagt till eller tagit bort annonser, så den har en uppdaterad tidslinje. <p>Det manifest som uppdaterats för en livedatabas och gamla annonsbrytningar togs bort från tidslinjen eller så upptäcktes nya annonsmöjligheter (referenspunkter). Mediespelaren försöker lösa och placera nya annonser på tidslinjen. </p><p> Använd den här händelsen för att kontrollera om tidslinjen har några uppdateringar (VOD ändras inte under uppspelning). Sedan kan du hämta tidslinjen med <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.html#getTimeline%28%29" format="html" scope="external"> MediaPlayer.getTimeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
