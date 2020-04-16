---
description: Klassen MediaResource representerar innehållet som ska läsas in av MediaPlayer-instansen.
seo-description: Klassen MediaResource representerar innehållet som ska läsas in av MediaPlayer-instansen.
seo-title: Skapa en medieresurs
title: Skapa en medieresurs
uuid: f34a11a3-dac2-405e-8632-1d9617cc019d
translation-type: tm+mt
source-git-commit: 1b7ec3759561159c55018b4b81f896ecc99a25e8

---


# Skapa en medieresurs {#create-a-media-resource}

För varje nytt videoinnehåll initierar du en MediaResource-instans med information om videoinnehållet och läser in medieresursen.

Klassen MediaResource representerar innehållet som ska läsas in av MediaPlayer-instansen.

1. Skapa en `MediaResource` genom att skicka information om mediet till `MediaResource` konstruktorn.

   Konstruktorn kräver följande parametrar `MediaResource` :

   <table id="table_22886D6770FB45E99D35D0B90E6CC302">
      <thead>
      <tr>
      <th colname="col1" class="entry"> Konstruktorparameter </th>
      <th colname="col2" class="entry"> Beskrivning </th>
      </tr>
      </thead>
      <tbody>
      <tr>
      <td colname="col1"> <span class="codeph"> url </span> </td>
      <td colname="col2"> En sträng som representerar URL:en för mediets manifest/spellista. </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> type </span> </td>
      <td colname="col2"> En av följande medlemmar i <span class="codeph"> MediaResource.Type- </span> uppräkningen, som motsvarar den angivna filtypen:
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282">
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS </span> - M3U8 </li>
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF </span> - ISO-basmediefilformat (MP4) </li>
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> DASH </span> - MPEG-DASH mediepresentationsbeskrivning (MPD) </li>
      </ul> </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> metadata </span> </td>
      <td colname="col2"> En instans av <span class="codeph"> Metadata- </span> klassen (en ordlisteliknande struktur), som kan innehålla ytterligare information om innehållet som ska läsas in, till exempel alternativt innehåll eller annonsinnehåll som ska placeras inuti huvudinnehållet. Om du använder annonsering ska du ställa in <span class="codeph"> AuditudeSettings </span> innan du använder konstruktorn. </td>
      </tr>
      </tbody>
   </table>

   >[!IMPORTANT]
   >
   >TVSDK stöder endast uppspelning av vissa typer av innehåll. Om du försöker läsa in någon annan typ av innehåll skickar TVSDK en felhändelse.
   >
   >För MP4-VOD-innehåll (video-on-demand) stöder inte TVSDK tricks play, ABR-strömning (adaptive bit rate), annonsinfogning, undertexter eller DRM.

   I följande kod skapas en `MediaResource` instans:

   ```java
   // To do: Create metadata here
   MediaResource res = new MediaResource(
     "https://www.example.com/video/some-video.m3u8",
     MediaResource.Type.HLS,
     metadata);
   ```

   När som helst efter det här steget kan du använda åtkomstmetoder (get-ters) för att undersöka resursens typ, URL-adress och metadata. `MediaResource`

1. Läs in medieresursen med något av följande alternativ:

   * MediaPlayer-instansen.
   * `MediaPlayerItemLoader` Mer information finns i [Läsa in en medieresurs med MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md).
   >[!IMPORTANT]
   >
   >Läs inte in medieresursen på en bakgrundstråd. De flesta TVSDK-åtgärder måste köras på huvudtråden, och om de körs på en bakgrundstråd kan åtgärden orsaka ett fel och avsluta åtgärden.
