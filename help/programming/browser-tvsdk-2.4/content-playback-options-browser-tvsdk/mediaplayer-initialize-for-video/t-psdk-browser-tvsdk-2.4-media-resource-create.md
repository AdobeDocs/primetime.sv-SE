---
description: Klassen MediaResource representerar innehållet som ska läsas in av MediaPlayer-instansen.
title: Skapa en medieresurs
exl-id: ab66255d-7848-479a-a8cd-c6113cdd7749
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Skapa en medieresurs {#create-a-media-resource}

Klassen MediaResource representerar innehållet som ska läsas in av MediaPlayer-instansen.

1. Skapa en `MediaResource` genom att skicka information om mediet till `MediaResource` konstruktor.

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
    <tr> 
    <th colname="col1" class="entry"> Konstruktorparameter </th> 
    <th colname="col2" class="entry"> Beskrivning </th> 
    </tr> 
    </thead>
    <tbody> 
    <tr> 
    <td colname="col1"> <p>url </p> </td> 
    <td colname="col2"> <p>En sträng som representerar URL:en för mediets manifest/spellista. </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>type </p> </td> 
    <td colname="col2"> <p>En av följande medlemmar i <span class="codeph"> MediaResource.Type </span> uppräkning som motsvarar den angivna filtypen: </p> <p> 
    <ul id="ul_E9689FA06DC94BF4848F16E1F2F01A59"> 
    <li id="li_83A14B96CDC648C6AF6F5FA745343E1F"> <span class="codeph"> MP4 </span> - ISO-format för basmediefil (MP4) </li> 
    <li id="li_FCD355151515412D9A78C3815DD09129"> <span class="codeph"> HLS </span> - M3U8 </li> 
    <li id="li_9D3D306D49264830AC6EFB1F49524A3B"> <span class="codeph"> DASH </span> - MPD </li> 
    </ul> </p> <p></p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>metadata </p> </td> 
    <td colname="col2"> <p>En instans av <span class="codeph"> Metadata </span> -klass, som kan innehålla anpassad information om innehållet som ska läsas in. Exempel på innehåll är alternativ eller annonsinnehåll som ska placeras inuti huvudinnehållet. Konfigurera <span class="codeph"> AuditudeSettings </span> innan den här konstruktorn används. Mer information finns i <a href="../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md">Ad-insertion-metadata</a>. </p> <p>Tips: Om det behövs kan du tvinga fram Flash-reservlösningar med <span class="codeph"> forceFlash </span> när en medieresurs skapas. Detta kan vara användbart eftersom inte alla funktioner (till exempel arbetsflöden för Live Ad) stöds i Browser TVSDK. Flash fallback används för att spela upp videoinnehåll. </p> </td> 
    </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >Webbläsarens TVSDK stöder endast uppspelning av vissa typer av innehåll. Om du försöker läsa in någon annan typ av innehåll skickar Browser TVSDK en felhändelse.

   I följande kod skapas en `MediaResource` instans:

   ```js
   //create a MediaResource instance pointing to some HLS content 
   Metadata metadata = //TODO: create metadata here 
   mediaResource = new AdobePSDK.MediaResource ( 
         "https://www.example.com/video/some-video.m3u8", 
         AdobePSDK.MediaResourceType.HLS,  
         metadata);
   ```

   >[!TIP]
   >
   >Du kan använda `MediaResource` accessorer (getters) för att undersöka resursens typ, URL och metadata.

1. Läs in din MediaPlayer-instans. Mer information finns i [Läsa in en medieresurs i MediaPlayer](../../content-playback-options-browser-tvsdk/mediaplayer-initialize-for-video/t-psdk-browser-tvsdk-2.4-media-resource-load.md).
