---
description: För varje nytt videoinnehåll initierar du en MediaResource-instans med information om videoinnehållet och läser in medieresursen. Klassen MediaResource representerar innehållet som ska läsas in av MediaPlayer-instansen.
title: Skapa en medieresurs
exl-id: cda70f91-7f30-4e37-9dfa-888b707e3d61
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Skapa en medieresurs {#create-a-media-resource}

För varje nytt videoinnehåll initierar du en MediaResource-instans med information om videoinnehållet och läser in medieresursen. Klassen MediaResource representerar innehållet som ska läsas in av MediaPlayer-instansen.

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
    <td colname="col2"> <p>En av följande medlemmar i <span class="codeph"> MediaResource.Type </span> uppräkning som motsvarar den angivna filtypen: 
    <ul id="ul_72636C41CA7E4538A3BE11A79E0282FC"> 
    <li id="li_070960200DEB40E992C58FCB8909AEA3"> <span class="codeph"> HLS </span> - M3U8 </li> 
    </ul> </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>metadata </p> </td> 
    <td colname="col2"> <p>En instans av <span class="codeph"> Metadata </span> -klass, som kan innehålla anpassad information om innehållet som ska läsas in. </p> <p>Exempel på innehåll är alternativ eller annonsinnehåll som ska placeras inuti huvudinnehållet. Konfigurera <span class="codeph"> AuditudeSettings </span>. Mer information finns i <a href="../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-insertion-metadata-set-up.md" format="dita" scope="local"> Ad Insertion-metadata </a>. </p> </td> 
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
   try { 
       // create a MediaResource instance pointing to some HLS content 
       Metadata metadata = //TODO: create metadata  
       MediaResource mediaResource = MediaResource.createFromUrl( 
         "https://www.example.com/video/some-video.m3u8",  
         MediaResource.Type.HLS,  
         metadata); 
   } catch(IllegalArgumentException ex) { 
       // this exception is thrown if the URL does not point  
       // to a valid url. 
   } 
   ```

   >[!TIP]
   >
   >Nu kan du använda `MediaResource` accessorer (getters) för att undersöka resursens typ, URL och metadata.

1. Läs in medieresursen med följande:

   * Din MediaPlayer-instans.

      Mer information finns i [Läsa in en medieresurs i MediaPlayer](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` Mer information finns i [Läsa in en medieresurs med MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).
   >[!IMPORTANT]
   >
   >Läs inte in medieresursen på en bakgrundstråd. De flesta TVSDK-åtgärder måste köras på huvudtråden, och om de körs på en bakgrundstråd kan åtgärden orsaka ett fel och avsluta åtgärden.
