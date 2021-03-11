---
description: Klassen MediaResource representerar innehållet som ska läsas in av MediaPlayer-instansen.
title: Skapa en medieresurs
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# Skapa en medieresurs {#create-a-media-resource}

För varje nytt videoinnehåll initierar du en MediaResource-instans med information om videoinnehållet och läser in medieresursen.

Klassen MediaResource representerar innehållet som ska läsas in av MediaPlayer-instansen.

1. Skapa en `MediaResource` genom att skicka information om mediet till konstruktorn `MediaResource`.

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> Konstruktorparameter </th> 
      <th colname="col2" class="entry"> Beskrivning </th> 
      </tr>
    </thead>
    =<tbody> 
      <tr> 
      <td colname="col1"><span class="codeph"> url</span> </td> 
      <td colname="col2"> <p>En sträng som representerar URL:en för mediets manifest/spellista. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> type</span> </td> 
      <td colname="col2"> <p>Ett av följande strängvärden som motsvarar den angivna filtypen: 
        <ul id="ul_7512E90B7B294EF9BFBA2D68DE678CBB"> 
        <li id="li_AA84434E84184A3D909552794B425ABD"><span class="codeph"> MP4</span> - ISO basmediefilformat (MP4) </li> 
        <li id="li_8A2F3752569344B59EE30303A8393488"><span class="codeph"> HLS</span> - M3U8 </li> 
        </ul> </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> metadata</span> </td> 
      <td colname="col2"> <p>En instans av klassen <span class="codeph"> Metadata</span> som kan innehålla anpassad information om innehållet som ska läsas in. </p> <p>Exempel på innehåll är alternativ eller annonsinnehåll som ska placeras inuti huvudinnehållet. Om du använder annonsering ska du ställa in <span class="codeph"> AuditudeSettings</span> innan du använder konstruktorn. Mer information finns i <a href="../../../tvsdk-1.4-for-desktop-hls/ad-insertion/ad-insertion-metadata/c-psdk-dhls-1.4-ad-insertion-metadata.md" format="dita" scope="local"> Ad Insertion-metadata</a>. </p> </td> 
      </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK stöder endast uppspelning av vissa typer av innehåll. Om du försöker läsa in någon annan typ av innehåll skickar TVSDK en felhändelse.
   >
   >För MP4-VOD-innehåll (video-on-demand) stöder inte TVSDK tricks play, ABR-strömning (adaptive bit rate), annonsinfogning, undertexter eller DRM.

   I följande kod skapas en `MediaResource`-instans:

   ```
   // To do: Create metadata here
   MyResource = new MediaResource(
            "https://www.example.com/video/some-video.m3u8", 
            "HLS",
            MyMetadata)
   ```

   >[!TIP]
   >
   >Nu kan du använda `MediaResource`-accessorer (getters) för att undersöka resursens typ, URL och metadata.

1. Läs in medieresursen med något av följande:

   * Din MediaPlayer-instans.

      Mer information finns i [Läs in en medieresurs i mediaplayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` Mer information finns i [Läs in en medieresurs i mediaplayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).

