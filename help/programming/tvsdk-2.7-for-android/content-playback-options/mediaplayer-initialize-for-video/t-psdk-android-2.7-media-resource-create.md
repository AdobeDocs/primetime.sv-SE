---
description: Klassen MediaResource representerar innehållet som ska läsas in av MediaPlayer-instansen.
title: Skapa en medieresurs
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Skapa en medieresurs {#create-a-media-resource}

För varje nytt videoinnehåll initierar du en MediaResource-instans med information om videoinnehållet och läser in medieresursen.

Klassen MediaResource representerar innehållet som ska läsas in av MediaPlayer-instansen.

1. Skapa en `MediaResource` genom att skicka information om mediet till konstruktorn `MediaResource`.

   Konstruktorn `MediaResource` kräver följande parametrar:

   <table id="table_22886D6770FB45E99D35D0B90E6CC302">
      <thead>
      <tr>
      <th colname="col1" class="entry"> Konstruktorparameter </th>
      <th colname="col2" class="entry"> Beskrivning </th>
      </tr>
      </thead>
      <tbody>
      <tr>
      <td colname="col1"> <span class="codeph"> url  </span> </td>
      <td colname="col2"> En sträng som representerar URL:en för mediets manifest/spellista. </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> type  </span> </td>
      <td colname="col2"> En av följande medlemmar i uppräkningen <span class="codeph"> MediaResource.Type </span>, som motsvarar den angivna filtypen:
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282">
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS  </span> - M3U8 </li>
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF  </span> - ISO basmediefilformat (MP4) </li>
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> DASH  </span> - MPEG-DASH mediepresentationsbeskrivning (MPD) </li>
      </ul> </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> metadata  </span> </td>
      <td colname="col2"> En instans av klassen <span class="codeph"> Metadata </span> (en ordlisteliknande struktur), som kan innehålla ytterligare information om innehållet som ska läsas in, till exempel alternativt innehåll eller annonsinnehåll som ska placeras inuti huvudinnehållet. Om du använder annonsering ska du ställa in <span class="codeph"> AuditudeSettings </span> innan du använder konstruktorn. </td>
      </tr>
      </tbody>
   </table>

   >[!IMPORTANT]
   >
   >TVSDK stöder endast uppspelning av vissa typer av innehåll. Om du försöker läsa in någon annan typ av innehåll skickar TVSDK en felhändelse.
   >
   >För MP4-VOD-innehåll (video-on-demand) stöder inte TVSDK tricks play, ABR-strömning (adaptive bit rate), annonsinfogning, undertexter eller DRM.

   I följande kod skapas en `MediaResource`-instans:

   ```java
   // To do: Create metadata here
   MediaResource res = new MediaResource(
     "https://www.example.com/video/some-video.m3u8",
     MediaResource.Type.HLS,
     metadata);
   ```

   När som helst efter det här steget kan du använda `MediaResource`-accessorer (getters) för att undersöka resursens typ, URL och metadata.

1. Läs in medieresursen med något av följande alternativ:

   * MediaPlayer-instansen.
   * `MediaPlayerItemLoader` Mer information finns i  [Läsa in en medieresurs med MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md).

   >[!IMPORTANT]
   >
   >Läs inte in medieresursen på en bakgrundstråd. De flesta TVSDK-åtgärder måste köras på huvudtråden, och om de körs på en bakgrundstråd kan åtgärden orsaka ett fel och avsluta åtgärden.
